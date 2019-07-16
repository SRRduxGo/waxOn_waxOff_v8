# waxOn_waxOff_v8
Guide to understand V8 internals and optimize JS

## Optimized code in JS frameworks
- https://www.youtube.com/watch?v=_VHNTC67NR8

    - [x] _Locating value of an object's property in memory is an expensive process_
    - [x] _shapes aka Hidden Classes in (Maps in V8)_
    - [x] _JSObject ⇨ has **Shape** ⇝ Every property in the **Shape** has <..property information.. ∋ offset::Writable::Enumerable::Configurable>_
    - [x] _**Shape**_  _reduces Memory footprints_
    - [x] _**Transtion chains in V8 ⇨ Chain of Shapes ⇨ Happen when dynamically Add/Delete properties from a JS object whose Shape was already defined when the Js object was initialized**_
    - [x] _**Transition chains ⇨ More lookup time by V8 Engine to find the property**_ 
    - [x] _Inline Caching (IC) ⇨ Every `function` has a **`Feedback Vector`** , which caches the **Shape** of the objects passed as arguments_
    - [x] _**`Feedback Vector`** caches `shape | properties | offset | state` of the argument object_
    - [x] _**`Feedback Vector`** ⇨ `state` cache  ⇨ can have one of the three values `monomorphic property access` | `polymorphic property access` | `megamorphic property access`_
    
    - [x] _**`monomorphic property access`** happens when `function` has been called with only one type of `shape` objects_
    - [x] _**`Monomorphic`** property access speeds are 100 times faster than **`Megamorphic`** property access in a function_
    - [x] _How **JS frameworks** make property access `monomorphic` :_
```javascript

/*
Here property access is NOT monomorphic
**/
type Element{
    fieldA;
    fieldB;
};
type Component{
    fieldC;
    fieldD;
}

/** both the structures above are 
combined to yield one Structure - Union of all */
 
 /*
Here property access IS monomorphic
**/
 
 type Node {
    tag: nodeType;
    
    fieldA | null;
    fieldB | null;   
    fieldC | null;
    fieldD | null;
    
 }
 

```

  - [x] _**BitFields** `Array of bits` _
  
  ```javascript
    let effectTag = 0b010100111 //167
  
  ```
   - [x] _**React** uses **BitFields** to encode side effects, each bit in the field signifies what side effect to perform_
   _ie, `UPDATE` `PLACEMENT` etc_
   
   - [x] _**Advantages of BitFields**_
        - _No need to allocate memory for JS objects and shapes_
        - _Simplified garbage collection_
        - _Smaller and Contiguous memory usage_
        - _Fast access using single bitwise operator_
   ```javascript
    const effectTag = 0b000000000010
    const effectTags  ={
        Placement: 0b000000000010,
        Update: 0b000000000100,
        PlacementAndUpdate: 0b000000001000
    };
    
    if(effectTag & effectTags.Placement){
        ...
    }
  
  ```
   - [x] _**Bloom Filters**_ _Data structure which answers `Definitely No` or `Maybe`
        - _used when answer is `no` most of the times_
















