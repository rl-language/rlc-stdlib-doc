# vector.rl

## cls Vector
```
 A memory contiguous datastructure similar to cpp vector.
 A vector is a list of elements. Just like cpp vector,
 the contents may be reallocated when added or deleated,
 so references elements are invalidated if the 
 vector is modified.
```

### Fields


### Methods

* fun `init() `
* fun `drop() `
* fun `assign(Vector<T> other) `
* fun `resize(Int new_size) `
```
 changes the size of the vector
 to be equal to `new_size`
 if the original size is larger
 than the new size, the extra 
 elements are destroyed
 
 if the original size is smaller
 than the new size, extra elements
 are constructed
```
* fun `back()  -> ref T`
```
 returns a reference to the
 last element of the vector
```
* fun `get(Int index)  -> ref T`
```
 returns a reference to the element
 with the provided index
```
* fun `set(Int index, T value) `
```
 assigns `value` to the element
 of the vector at the provided
 index
```
* fun `append(T value) `
```
 appends `value` to the 
 end of the vector
```
* fun `empty()  -> Bool`
```
 returns true if the
 size of the vector is equal
 to zero
```
* fun `clear() `
```
 erases all the elements
 of the vector
```
* fun `pop()  -> T`
```
 removes the last element
 of the vector and returns
 it by copy
```
* fun `drop_back(Int quantity) `
```
 removes `quantity` elements
 from the back of the vector
```
* fun `erase(Int index) `
```
 erase the element with the provided
 `index`
```
* fun `size()  -> Int`

## cls BoundedVector
```
 A bounded vector is a wrapper
 around a vector that prevents 
 the size of the vector to ever 
 exced `max_size`
 this class is usefull when used
 for machine learning techniques, 
 since it allows the machine learning
 to know the maximal possible size
 of this vector when converted to
 a tensor
```

### Fields


### Methods

* fun `assign(BoundedVector<T, max_size> other) `
* fun `resize(Int new_size) `
```
 identical to Vector::resize,
 except `new_size` is clamped
 to be at most `max_size`
```
* fun `max_size()  -> Int`
```
 returns the maximal possible
 size of this vector
```
* fun `back()  -> ref T`
```
 same as vector::back
```
* fun `get(Int index)  -> ref T`
```
 same as vector::get
```
* fun `set(Int index, T value) `
```
 same as vector::set
```
* fun `append(T value) `
```
 append `value` to the end
 of the vector, but only if
 doing so would not excede
 max vector maximal size
```
* fun `empty()  -> Bool`
```
 same as vector::empty
```
* fun `clear() `
```
 same as vector::clear
```
* fun `pop()  -> T`
```
 same as vector::pop
```
* fun `drop_back(Int quantity) `
```
 same as vector::drop_back
```
* fun `erase(Int index) `
```
 same as vector::erase
```
* fun `size()  -> Int`
```
 same as vector::size
```

