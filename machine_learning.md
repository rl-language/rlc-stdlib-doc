# machine_learning.rl

## cls Hidden
```
 A Hidden object rapresents a object that is not visibile to machine
 learning algorithms. For example a machine learning algorithms learning
 to play black jack should not have access to the deck of cards, so it can be wrapped into a hidden to achieve that effect
```

### Fields

* T value

### Methods

* fun `assign(T content) `

## cls HiddenInformation

### Fields

* T value
* Int owner

### Methods

* fun `assign(T content) `


### Free functions

* fun `write_in_observation_tensor<T>(Hidden<T> obj, Int observer_id, Vector<Float> output, Int index) `
```
 since the underlying object is hidden, this function does nothing.
```
* fun `size_as_observation_tensor<T>(Hidden<T> obj)  -> Int`
```
 since the underlying object is hidden, always returns zero 
```
* fun `append_to_vector<T>(Hidden<T> to_add, Vector<Byte> output) `
* fun `parse_from_vector<T>(Hidden<T> to_add, Vector<Byte> output, Int index)  -> Bool`
* fun `append_to_string<T>(Hidden<T> to_add, String output) `
* fun `parse_string<T>(Hidden<T> to_add, String input, Int index)  -> Bool`
* fun `write_in_observation_tensor<T>(HiddenInformation<T> obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor<T>(HiddenInformation<T> obj)  -> Int`
