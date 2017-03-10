# CodeStyle-ObjC
Objective C Code Style

### isEqual Implementation

Given hierarchy B -> A -> NSObject

```objc
// A's isEqual:
- (BOOL)isEqual:(id)object {
    if (self == object) {
        return YES;
    }
    if (![object isKindOfClass:A.class]) {
        return NO;
    }
    return [self isEqualToA:(A *)object];
}

// B's isEqual:
- (BOOL)isEqual:(id)object {
    // if the superclass doesn't like it then we're not equal
    if(![super isEqual:object]) {
        return NO;
    }
    // if it's not an instance of the subclass, then trust the superclass
    // it's equal there, so we consider it equal here
    if(![object isKindOfClass:B.class]) {
        return YES;
    }
    // it's an instance of the subclass, the superclass properties are equal
    // so check for -isEqualToB:
    return [self isEqualToB:(B *)object];
}
```
