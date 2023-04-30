# Vue TypeScript Bootcamp - README

This project is the result of my learning journey with Vue.js and TypeScript. In this README, I will share some of the key concepts I've learned throughout my learning process. However, I will not cover everything comprehensively, as the aim is to demonstrate what I've learned so far. Please note that this project will continue to evolve, incorporating more TypeScript techniques in the future.

## Table of Contents

1. [Reactive Variables with Type Inference](#reactive-variables-with-type-inference)
   - [Composition API and Script Setup](#composition-api-and-script-setup)
   - [Ref() and Reactive()](#ref-and-reactive)
   - [Type Inference](#type-inference)
   - [Interfaces and Type Annotations](#interfaces-and-type-annotations)
   - [Handling Null or Undefined Values](#handling-null-or-undefined-values)
2. [Callback Functions and Type Inference](#callback-functions-and-type-inference)
   - [Functions and Parameters](#functions-and-parameters)
   - [Function Return Type Inference](#function-return-type-inference)
   - [Inline Function Type Inference](#inline-function-type-inference)
3. [Props with Compiler Macros](#props-with-compiler-macros)
   - [Defining Props and Types with `defineProps`](#defining-props-and-types)
   - [Default Prop Values with `withDefaults`](#default-prop-values)
4. [Type-Safe Emit](#type-safe-emit)
   - [Emit](#emit)
   - [Inline Event Handling](#inline-event-handling)
5. [Conclusion](#conclusion)

## Reactive Variables with Type Inference <a name="reactive-variables-with-type-inference"></a>

### Composition API and Script Setup <a name="composition-api-and-script-setup"></a>

The Composition API is a new approach to organizing component logic in Vue 3. The "script setup" syntax further simplifies the use of the Composition API, eliminating the need to define a **setup()** function.

### Ref() and Reactive() <a name="ref-and-reactive"></a>

**ref()** and **reactive()** are two fundamental functions of the Composition API that allow creating reactive variables. **ref()** is used for individual values, while **reactive()** is used for objects.

### Type Inference <a name="type-inference"></a>

TypeScript is capable of automatically inferring the types of variables in most cases. For example, when using **ref(0)**, TypeScript understands that it's a **Ref<number>** type. This is very helpful in reducing code verbosity and maintaining readability.

### Interfaces and Type Annotations <a name="interfaces-and-type-annotations"></a>

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

### Handling Null or Undefined Values <a name="handling-null-or-undefined-values"></a>

When working with TypeScript, sometimes you need to handle null or undefined values. For example, if you expect to fetch a value from an HTTP service, you might initially set the value to null. In this case, you need to specify the type of the variable using a type union:

```typescript
const count = ref<number | null>(null)
```

## Callback Functions and Type Inference <a name="callback-functions-and-type-inference"></a>

In this section, we'll explore how TypeScript can infer the types of callback functions and the different ways of using functions in TypeScript.

### Functions and Parameters <a name="functions-and-parameters"></parameters"></a>

When working with functions in TypeScript, you can often rely on type inference. However, there might be situations where type inference fails, and you need to provide explicit type annotations for your function parameters. For example, consider this addCount function:

```typescript
function addCount(num: number) {
  if (count.value !== null) {
    count.value += num;
  }
}
```

By annotating the parameter num with its expected type number, TypeScript can properly understand and validate the function usage.

### Function Return Type Inference <a name="function-return-type-inference"></a>

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

### Inline Function Type Inference <a name="inline-function-type-inference"></a>

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

## Props with Compiler Macros <a name="props-with-compiler-macros"></a>

In Vue.js and TypeScript, we can define props and their types using the `defineProps` function, which is a compiler macro. Compiler macros are only called during compile-time and don't appear in the runtime code. They can only be used within `<script setup>`.

### Defining Props and Types with `defineProps` <a name="defining-props-and-types"></a>

To define props and their types using `defineProps`, we can either use a generic type argument or a function argument.

Using a generic type argument:

```typescript
interface Props {
  limit: number,
  alertMessageOnLimit: string
}

const props = defineProps<Props>()
```

Using a function argument:

```typescript
const props = defineProps({
  limit: { type: Number, required: true },
  alertMessageOnLimit: { type: String, required: true },
})
```

Both of these methods provide static type checking for props. However, using a generic type argument is the recommended method as it's in pure TypeScript.

### Default Prop Values with withDefaults <a name="default-prop-values"></a>

To define default values for props, we can use the withDefaults function in combination with defineProps. First, we need to make the prop optional in the interface:

```typescript
interface Props {
  limit: number;
  alertMessageOnLimit?: string;
}
```

Next, we use withDefaults to set the default value for the optional prop:

```typescript
const props = withDefaults(defineProps<Props>(), {
  alertMessageOnLimit: 'can not go any higher',
})
```

By using withDefaults and defineProps in a function composition pattern, we can define default values for optional props in a clean and efficient way.

## Type-Safe Emit <a name="type-safe-emit"></a>
### Emit <a name="emit"></a>
- Introduction to the new annotation syntax for emitted events (emit)
- Using defineEmits to define the events the component is allowed to emit

```typescript
<script setup lang="ts">
const emit = defineEmits<{ 
  (event: 'add-count', num: number): void
  (event: 'reset-count'): void
}>()
</script>
```

Examples of how to modify the template to emit events and handle errors if emitting unspecified events

```typescript
<template>
  <p>
    <button @click="emit('add-count', 1)">Add</button>
    <button @click="emit('reset-count')">Reset</button>
  </p>
</template>
```

Explanation of how Vue derives the type of function required for handling the emitted event

### Inline Event Handling <a name="inline-event-handling"></a>
Handling events inline in the parent component

```typescript
<ControlBar 
  @add-count="addCount"
  @reset-count="count = 0"
></ControlBar>
```

Explanation of how statements are compiled into functions and accepted as callbacks

## Conclusion <a name="conclusion"></a>

These are just a few of the key concepts I've learned during my Vue.js and TypeScript learning journey. There are undoubtedly other interesting topics to explore, but this README should serve as a starting point to demonstrate my current knowledge. As mentioned earlier, this project will continue to incorporate more TypeScript techniques as it progresses. I will continue learning and improving my skills over time.
