AutoSave ![CircleCI branch](https://img.shields.io/circleci/project/github/RedSparr0w/node-csgo-parser/master.svg?style=flat-square)
===========

Automatically save, load, and sync NBT data with a easy to use, easy to extend, annotation based API.

## How To Use

### Label your fields

Simply annotate any fields that need to be saved with `@Store`.

```java
public class MyObject {
    
    @Store
    private String name;
    
    @Store
    private int counter;
}
```

### Serialize With Ease

The (de)serialization API is very simple, only a single line of code!

#### To write an object to NBT:

```java
NBTTagCompound tag = new NBTTagCompound();
Writer.write(tag, object);
```

#### To read an object from NBT:

```java
Reader.read(tag, object);
```

### Automatic recursive serializer support

```java
@Storable
public class StorableExample {
    
    @Store
    private String name;
}

public class Wrapper {
    
    @Store
    private StorableExample storable;
}

Writer.write(tag, new Wrapper()); // This will work!
```

### Extend the supported field types

```java
Registry registry = new Registry();
registry.register(new HandleMyObject());

...

class Wrapper {

    @Store
    private MyObject myObject = new MyObject();
}

NBTTagCompound tag = new NBTTagCompound();
Writer.write(registry, tag, new Wrapper());
```

##### For more information, refer to the javadocs.