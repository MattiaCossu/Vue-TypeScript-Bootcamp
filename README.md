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

## Conclusion

These are just a few of the key concepts I've learned during my Vue.js and TypeScript learning journey. There are undoubtedly other interesting topics to explore, but this README should serve as a starting point to demonstrate my current knowledge. As mentioned earlier, this project will continue to incorporate more TypeScript techniques as it progresses. I will continue learning and improving my skills over time.