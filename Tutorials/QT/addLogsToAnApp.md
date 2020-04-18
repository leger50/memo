# Qt - Externalize logs of an application

## Exemple
```C
#include "mainwindow.h"

#include <QApplication>

// Get the default Qt message handler.
static const QtMessageHandler QT_DEFAULT_MESSAGE_HANDLER = qInstallMessageHandler(nullptr);

static const QMap<QtMsgType, QString> initMapQtMsgType(){
    QMap<QtMsgType, QString> map;

    map.insert(QtDebugMsg, "Debug");
    map.insert(QtInfoMsg, "Infos");
    map.insert(QtWarningMsg, "Warnings");
    map.insert(QtCriticalMsg, "Critical");
    map.insert(QtFatalMsg, "Fatal");

    return map;
}
static const QMap<QtMsgType, QString> mapQtMsgType = initMapQtMsgType();

void firmwareUpdateCustomMessageHandler(QtMsgType type, const QMessageLogContext &context, const QString &msg)
{
    // Handle the messages!
    QByteArray localMsg = msg.toLocal8Bit();
    const char *file = context.file ? context.file : "";
    const char *function = context.function ? context.function : "";

    QString msgType = mapQtMsgType.value(type);
    QString formattedMessage = QString("[%1] %2 (%3:%4, %5\n");

    QTime time = QTime::currentTime();
    QString formattedTime = time.toString("hh:mm:ss.zzz");

    QString logMessage = formattedMessage.arg(formattedTime).arg(localMsg.constData()).arg(file).arg(context.line).arg(function);
    QString logFolder = QString("./logs/%1/").arg(QDate::currentDate().toString("dd-MM-yyyy"));

    QDir dir; dir.mkpath(logFolder);

    QFile outLogFile; QTextStream outLogStr(&outLogFile);
    outLogFile.setFileName(logFolder + msgType + ".log");
    outLogFile.open(QFile::Append);
    outLogStr << logMessage;
    outLogFile.close();

    // Call the default handler.
    (*QT_DEFAULT_MESSAGE_HANDLER)(type, context, msg);
}

int main(int argc, char *argv[])
{
    qInstallMessageHandler(firmwareUpdateCustomMessageHandler);
    QApplication app(argc, argv);

    MainWindow window;
    window.show();

    return app.exec();
}
```