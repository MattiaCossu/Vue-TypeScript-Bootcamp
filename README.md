# Vue TypeScript Bootcamp - README 

This project is the result of my learning journey with Vue.js and TypeScript. In this README, I will share some of the key concepts I've learned throughout my learning process. However, I will not cover everything comprehensively, as the aim is to demonstrate what I've learned so far. Please note that this project will continue to evolve, incorporating more TypeScript techniques in the future.

## Ket Concepts

### Composition API and Script Setup
The Composition API is a new approach to organizing component logic in Vue 3. The "script setup" syntax further simplifies the use of the Composition API, eliminating the need to define a <b>setup()</b> function.

### Ref() and Reactive()
<b>ref()</b> and <b>reactive()</b> are two fundamental functions of the Composition API that allow creating reactive variables. <b>ref()</b> is used for individual values, while <b>reactive()</b> is used for objects.

### Type Inference
TypeScript is capable of automatically inferring the types of variables in most cases. For example, when using <b>ref(0)</b>, TypeScript understands that it's a <b>Ref<number></b> type. This is very helpful in reducing code verbosity and maintaining readability.

### Interfaces and Type Annotations
In some cases, it is helpful to define custom interfaces to describe the shape of an object. For example, we've defined an AppInfo interface:
```typescript
interface AppInfo {
  name: string;
  slogan: string;
}
```
By using this interface, we can annotate the type of a variable to improve code readability:
```typescript
const appInfo: AppInfo = reactive({
  name: 'Counter',
  slogan: 'an app you can count on',
})
```

### Handling Null or Undefined Values
When working with TypeScript, sometimes you need to handle null or undefined values. For example, if you expect to fetch a value from an HTTP service, you might initially set the value to null. In this case, you need to specify the type of the variable using a type union:
```typescript
const count = ref<number | null>(null)
```

## Callback Functions and Type Inference
In this section, we'll explore how TypeScript can infer the types of callback functions and the different ways of using functions in TypeScript.

### Functions and Parameters
When working with functions in TypeScript, you can often rely on type inference. However, there might be situations where type inference fails, and you need to provide explicit type annotations for your function parameters. For example, consider this addCount function:
```typescript
function addCount(num: number) {
  if (count.value !== null) {
    count.value += num;
  }
}
```
By annotating the parameter num with its expected type number, TypeScript can properly understand and validate the function usage.

### Function Return Type Inference
TypeScript can also infer the return type of a function. For instance, when using a computed property:
```typescript
const nextCount = computed(() => {
  if (count.value !== null) {
    return count.value + 1;
  }
  return null;
})
```
Since TypeScript knows that count.value is a number, it can deduce that number + 1 is still a number. Therefore, there's no need to manually specify the return type of the function.

### Inline Function Type Inference
Type inference can work effectively when a callback function is passed inline. For example:
```typescript
fetchCount((initialCount) => {
  count.value = initialCount;
})
```
In this case, TypeScript can deduce the parameter type of the inline callback function, as it knows the type of the parameter that fetchCount accepts.

However, if you define the callback function separately, TypeScript might not be able to infer the type, and you may need to provide an explicit type annotation:
```typescript
const cb = (initialCount: number) => {
  count.value = initialCount;
}

fetchCount(cb)
```
In summary, TypeScript's type inference can effectively deduce the types of callback functions and their parameters in most cases. It's important to remember to provide explicit type annotations when type inference fails to give TypeScript enough information to infer the correct types.

## Conclusion
These are just a few of the key concepts I've learned during my Vue.js and TypeScript learning journey. There are undoubtedly other interesting topics to explore, but this README should serve as a starting point to demonstrate my current knowledge. As mentioned earlier, this project will continue to incorporate more TypeScript techniques as it progresses. I will continue learning and improving my skills over time.