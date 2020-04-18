# Qt - Use own class like an HashKey

Sometimes, we need a key who can have more than 1 element for `QHashMap`, here an exemple for an _HashKey_

## Exemple

Here an exemple for a QrCode capacity, the size of an QrCode message depends on his _version_ and his _level of error correction_. We can't calculate the capacity, this is fixed, so wee need to store capacity information somewhere, I used `QHashMap`.

### KeyCapacity.h
```C
#ifndef KEYCAPACITY_H
#define KEYCAPACITY_H

#include <QtGlobal>
#include <QString>
#include <QHash>
#include <QDebug>

class KeyCapacity
{

public:
    KeyCapacity(quint8 version, quint8 levelErrorCorrection)
        : m_version(version), m_levelErrorCorrection(levelErrorCorrection){ }

    quint8 version() const { return m_version; }
    quint8 levelErrorCorrection() const { return m_levelErrorCorrection; }

    inline bool operator==(const KeyCapacity &otherKey) const
        { return m_version == otherKey.m_version && m_levelErrorCorrection == otherKey.m_levelErrorCorrection; }
    inline bool operator!=(const KeyCapacity &otherKey) const
        { return !operator==(otherKey); }

private:
    quint8 m_version;
    quint8 m_levelErrorCorrection;
};

inline uint qHash(const KeyCapacity &key) {
    QString hash = QString("%1|%2").arg(key.version()).arg(key.levelErrorCorrection());
    return qHash(hash);
}

inline QDebug operator<<(QDebug debug, const KeyCapacity &key)
{
    QDebugStateSaver saver(debug);
    debug.nospace() << '(' << key.version() << ", " << key.levelErrorCorrection() << ')';

    return debug;
}

#endif // KEYCAPACITY_H
```

### How to use
```C
//Create
QHash<KeyCapacity, int> map;
//Insert
map.insert(KeyCapacity(1, ECC_LOW), 41);
//Get value
map.value(KeyCapacity(version, levelEcc));
```