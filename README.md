# waxOn_waxOff_v8
Guide to understand V8 internals and optimize JS

## Optimized code in JS frameworks
- https://www.youtube.com/watch?v=_VHNTC67NR8

    - [x] _Locating value of an object's property in memory is an expensive process_
    - [x] _shapes aka Hidden Classes in (Maps in V8)_
    - [x] _JSObject ⇨ has **Shape** ⇝ Every property in the **Shape** has <..property information.. ∋ offset::Writable::Enumerable::Configurable>_
    - [x] _**Shape**_  _reduces Memory footprints_
    - [x] _**Transtion chains in V8 ⇨ Chain of Shapes ⇨ Happen when dynamically Add/Delete properties from a JS object whose Shape was already defined when the Js object was initialized**_
    - [x] _**Transition chains ⇨ More look uptime by V8 Engine to find the property**_ 
    
