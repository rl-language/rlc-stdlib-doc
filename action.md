# action.rl


### Free functions

* fun `can_apply_impl<FrameType, ActionType>(ActionType action, FrameType frame)  -> Bool`
* fun `apply<FrameType, ActionType>(ActionType action, FrameType frame) `
* fun `apply<FrameType, ActionType>(Vector<ActionType> action, FrameType frame)  -> Bool`
* fun `parse_and_execute<FrameType, AllActionsVariant>(FrameType state, AllActionsVariant variant, Vector<Byte> input, Int read_bytes) `
* fun `parse_actions<AllActionsVariant>(AllActionsVariant variant, Vector<Byte> input, Int read_bytes)  -> Vector<AllActionsVariant>`
* fun `parse_actions<AllActionsVariant>(AllActionsVariant variant, String input)  -> Vector<AllActionsVariant>`
* fun `parse_action_optimized<AllActionsVariant>(AllActionsVariant variant, Vector<Byte> input, Int read_bytes)  -> Bool`
```
 parses actions taking only one byte and by taking taking the reminder of the parsed number divided by the number of actions, so that no action is ever marked as invalid
```
* fun `parse_actions<AllActionsVariant>(AllActionsVariant variant, Vector<Byte> input)  -> Vector<AllActionsVariant>`
* fun `parse_and_execute<FrameType, AllActionsVariant>(FrameType state, AllActionsVariant variant, Vector<Byte> input) `
* fun `gen_python_methods<FrameType, AllActionsVariant>(FrameType state, AllActionsVariant variant) `
```
 method that bust be present in binary to ensure that all methods 
 required by rlc-learn are available
```
* fun `load_action_vector_file<ActionType>(String file_name, Vector<ActionType> out)  -> Bool`
* fun `enumerate(Bool b, Vector<Bool> output) `
* fun `enumerate<T : Enum>(T b, Vector<T> output) `
* fun `enumerate<T>(T obj)  -> Vector<T>`
* fun `write_in_observation_tensor(Int value, Int min, Int max, Vector<Float> output, Int index) `
* fun `write_in_observation_tensor(Int obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor(Int obj)  -> Int`
* fun `write_in_observation_tensor(Float obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor(Float obj)  -> Int`
* fun `write_in_observation_tensor(Bool obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor(Bool obj)  -> Int`
* fun `write_in_observation_tensor(Byte obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor(Byte obj)  -> Int`
* fun `write_in_observation_tensor<T, X : Int>(T[X] obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor<T, X : Int>(T[X] obj)  -> Int`
* fun `write_in_observation_tensor<T>(Vector<T> obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor<T>(Vector<T> obj)  -> Int`
* fun `write_in_observation_tensor<T, max_size : Int>(BoundedVector<T, max_size> obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor<T, max_size : Int>(BoundedVector<T, max_size> obj)  -> Int`
* fun `write_in_observation_tensor<min : Int, max : Int>(BInt<min, max> obj, Int observer_id, Vector<Float> output, Int index) `
* fun `size_as_observation_tensor<min : Int, max : Int>(BInt<min, max> obj)  -> Int`
* fun `to_observation_tensor<T>(T obj, Int observer_id, Vector<Float> output) `
* fun `to_observation_tensor<T>(T obj, Int observer_id, Vector<Float> output, Int written_bytes) `
* fun `to_observation_tensor<T>(T obj, Int observer_id)  -> Vector<Float>`
* fun `observation_tensor_size<T>(T obj)  -> Int`
## trait ApplicableTo
* fun `apply(ActionType action, FrameType frame) `

## trait Enumerable
```
 trait that must be implemented by a type to enumerate all
 possible values of that types (ex: enumerate(bool) return 
 {true, false})
 
 this is used by machine learning techniques that need to
 enumerate all possible actions.
```
* fun `enumerate(T obj, Vector<T> output) `

## trait Tensorable
```
 trait that must be implemented to specify how
 a given type is to be converted into a tensor
 for machine learning consumptions. The encoding
 should be, when possible, one-hot encoding.
```
* fun `write_in_observation_tensor(T obj, Int observer_id, Vector<Float> output, Int counter) `
* fun `size_as_observation_tensor(T obj)  -> Int`

## trait Enum
* fun `max(T obj)  -> Int`
* fun `is_enum(T obj)  -> Bool`
* fun `as_int(T obj)  -> Int`
* fun `from_int(T obj, Int new_value) `

