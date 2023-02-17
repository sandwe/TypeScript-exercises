# TypeScript-exercises

> [TypeScript exercises](https://typescript-exercises.github.io/)의 단계별 에러를 해결하고, 해결 과정을 정리합니다.

## 목차

<br />

## 1번

> unknown으로 정의된 User의 타입을 정의하는 문제

### 문제

```ts
/*
Intro:

    We are starting a small community of users. For performance
    reasons we have decided to store all users right in the code.
    This way we can provide our developers with more
    user-interaction opportunities. With user-related data, at least.
    All the GDPR-related issues will be solved some other day.
    This would be the base for our future experiments during
    these exercises.

Exercise:

    Given the data, define the interface "User" and use it accordingly.
*/

export type User = unknown;

export const users: unknown[] = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
];

export function logPerson(user: unknown) {
  console.log(` - ${user.name}, ${user.age}`);
}

console.log("Users:");
users.forEach(logPerson);
```

### 풀이

```ts
export interface User {
  name: string;
  age: number;
  occupation: string;
}

export const users: User[] = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
];

export function logPerson(user: User) {
  console.log(` - ${user.name}, ${user.age}`);
}

console.log("Users:");
users.forEach(logPerson);
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/KYDwDg9gTgLgBASwHY2FAZgQwMbDgVQGc04BvAWACg4a4lMBbYALjkJimQHMBuK2uJi4s6AVwYAjNH2q0I2bKLCYYCCElbtOSXlQC+VKqEiw42dezijiUQqyJoA2gF04AXjiP+tCrIE16JlYAcgBZTBA4UOtUKAZMJCRggBpvf0FhVgAmAFZUv395RWVVdRCAYQALBAYkYABPNgB3YGAwYLS4PXyBX3SAxhFggGkVPFCAH4AbKbQUzoEhESyAZh7+oqUVNQ04YIBBLXVMURgOgoNKZxkjcGh4dFEkbFKkOCmILgAFNEJ1AAprGh7DYAJRkTrmJB-WYAOg+XH+AAM4ABaOAAElIQKgsMCwG6mOxNlhSz0SNBMkuVChMOA8M+-2CDlszGClKoOMIsPQ0AAojhKv8ET9bOoOZQgA)

- name, age, occupation 속성을 갖는 **user 객체**의 타입을 정의하기 위해 `interface` 적용

## 2번

> Union Type 정의하는 문제

### 문제

```ts
/*

Intro:

    All 2 users liked the idea of the community. We should go
    forward and introduce some order. We are in Germany after all.
    Let's add a couple of admins.

    Initially we only had users in the in-memory database. After
    introducing Admins, we need to fix the types so that
    everything works well together.

Exercise:

    Type "Person" is missing, please define it and use
    it in persons array and logPerson function in order to fix
    all the TS errors.

*/

interface User {
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  name: string;
  age: number;
  role: string;
}

export type Person = unknown;

export const persons: User[] /* <- Person[] */ = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
];

export function logPerson(user: User) {
  console.log(` - ${user.name}, ${user.age}`);
}

persons.forEach(logPerson);
```

### 풀이

```ts
interface User {
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  name: string;
  age: number;
  role: string;
}

export type Person = User | Admin;

export const persons: Person[] = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
];

export function logPerson(user: Person) {
  console.log(` - ${user.name}, ${user.age}`);
}

persons.forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/types-from-types.html
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/PQKgsAUJCSB2AuAnA9gLkpABNzBBANvpgEyYCuAzgKaIWb4CWA1lQCabwAWVmDrVAQ0zIAZh26YAxsgC2MsrAbwAngDpMAdR4VOyMvnYBzZFhwjkiAO4DE7AbHYMEKVmUnbZPC-0TqtmGx4nTABxGhl7ZQCReBoAwlVTbAAZKngAcjoBVjspPQAHfC8xbJknCkSoCBxMOCUGAUIoyy9YfCjObPJqWl5YcSDYAFoZKhkLKNYBeAEAIwFqdVwYmiS+pGRXSSdDPFYy2AoAGkwWzFgqNg5kTBEGAA8BjmV8qjoKG65ptaoANxplFwdqcLEw6C1CNdDGluL4MBAAKL3GjbajoKo1AAqLx4ACIAAo0D6wXG8OhlCgUHYnQqCaiYfh3C68eABBzdKhrJR9TCvWjIQ4BRCIARRezsfDIQyE-n9EQKSTwBgCnneOLwG53e5rRpELg8TEAZUwNBQtEqkBAwHhTliiBEAncmAAqj1MABvNawASjVCYChIHYAbh10L9sDIMlmNBD1RwyEkkjI+WmytgfoDiGDkAAvjaEDQHU7cPtgp649hvb7-YHYIZYzUBGHzpHo4gGzgUEUM7X67n4VR7vkLKyVK9MDLiZgALwut0AHz2B1jkEHw8QrOkh1ZfOJFD9k4FAG0ALozzBHtblmo1KtUP3pACyAkej8odoisFg6SOa0bzeIABWX8KxvBMkxTJUBQfABhTgGBkC4ogoFoqHydI1hzECamvG9Kx9e9MHSAApeweAAEWQKgfz-HAm0IgBmYhsLwzAu0I9ISwOBhM2mCwMNArCr1o-Dq3SABpaYeEfAAfwgaBo0D-0I4gGJYvDwOTVNoKI3BMwFAQyAyTD1I9ETzgIh8ACFEDcHgNAYQgeMU1iAmbAA2AAWUyanYh8NAsAx-QEf5EAEmo8wgE8VwgNcR1uBUoP6SVpSJAUAApKBoA80tgABKMzQK3D4ilUFL0oAA0wIZMAAEndLLfDvLC6oanpVHonMKry2NIsgXcBQqcxEARR1OHSlLD3ymLgGAWp+kkBYgjEZQ9CFbR4DcJh0VmzBOHgeB8n3WbLFO1QxzeSQs3yeB8HsQxVAsQxgFYBMKGAToHFmZBkCYYBiGAC6KCGEQUBkIYgdUfaZHwSAgA)

- `persons` 배열을 순회하며 `logPerson` 함수를 호출하고, 각 `user` 객체의 `name`, `age` 속성을 참조하고 있다.
- `persons`는 `User` 또는 `Admin` 타입을 갖는 객체들로 이루어진 배열로 **Union Type**을 떠올리게 됨.
- Union Type인 값 `user`에서는 `User`, `Admin` 타입의 공통 속성에만 접근 가능하다.
    <img width="589" alt="스크린샷 2023-02-17 오전 11 18 09" src="https://user-images.githubusercontent.com/79586634/219538235-6713ae1f-df6c-47c6-845b-63d3b23ff53b.png">


- 값이 A | B 타입을 가지면, A와 B 둘다 갖는 속성을 가지고 있다는 것은 확실하기 때문.
- 현재 코드에서는 공통 속성인 `name`, `age`만 참조하므로 가능하다.

<br />

## 3번

> 타입 가드(Type Guard) 하는 문제

### 문제

```ts
/*

Intro:

    Since we already have some of the additional
    information about our users, it's a good idea
    to output it in a nice way.

Exercise:

    Fix type errors in logPerson function.

    logPerson function should accept both User and Admin
    and should output relevant information according to
    the input: occupation for User and role for Admin.

*/

interface User {
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  name: string;
  age: number;
  role: string;
}

export type Person = User | Admin;

export const persons: Person[] = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
];

export function logPerson(person: Person) {
  let additionalInformation: string;
  if (person.role) {
    additionalInformation = person.role;
  } else {
    additionalInformation = person.occupation;
  }
  console.log(` - ${person.name}, ${person.age}, ${additionalInformation}`);
}

persons.forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing
```

### 풀이

```ts
interface User {
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  name: string;
  age: number;
  role: string;
}

export type Person = User | Admin;

export const persons: Person[] = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
];

export function logPerson(person: Person) {
  let additionalInformation: string;
  if ("role" in person) {
    additionalInformation = person.role;
  } else {
    additionalInformation = person.occupation;
  }
  console.log(` - ${person.name}, ${person.age}, ${additionalInformation}`);
}

persons.forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/PQKgsAUJCSB2AuAnA9gLkpABNzBlAlrAMYCmmA7mQIYA2iJVAJgJ6YAWVAbmQM7IC2ZZADNM8NtUaN88fMli0sOQsOSJ+VWfMxUARsgCu8TIcSYDPEoh4AaTDIDkPHZgDmyZI3uMGS7PGQTIwAHI3tjQhdYfFIKKmYAOgwIAFEADysifEt0KAgcTAAxfDSxZmCyKxRre1hMGmRXAAUrPjrhA2ItWCS8gobm1u0Orrk6njZDGi8qIlJg431xTABVSzMqWC8AQUZ+Qj8dLcwJqa9DeFDjehoSTk2I2FV1TTGdObVpWFcxZEPxMiEK6oExzAzBV7DNSrdZHLwoW6YZ6YXb7HrJEDAZKEeBWYSzMhrKyYADehwUghBPCQhFcAG5DlRXCQQbADPxdFYGfkcMgwRDulSad9uQBfbEIPEElF7SJknnYCksk7C+mM5ms9mcxDcgoI5XUxC0sXJEhpYJqYzwcpkFrWbQAXhhxIAPjK0dzIGaLYhjER5NTMBV7bAeCC7W0ANoAXUwTsjh3lBQKSpBDgAslRSumLLiXrBYA4bIcCkzlQAmACsxYVyb5RHBkNgaYAwmx8PxYCRWDxKCRgg5DqKawUk8nFVRKZgHAApTZkAAiyBIRZLODLIIAzOWR+PMPq06jCNkkJo1IPa8PE2uJ1OHABpTRkdMAH5ot0Qq9rpY1mHLm93cd60bQVp22Q15CoIwLwKK9azHcdU2nAAhRADFiAB1fB32yL89x0X8ADYABZAOTA9pwwtRphOLgrBgnBxQgaNPQgb1LSRToiG6epGgjeQAApgzacMhlgABKUlDluYwmGkbpaDgZ4NFAw1jUOfBRAEhx9QcWogzEySEOTOSZDGRSnjUFS3idYT5ASfVdUYzASBoSwpO-dcpDMyCaCUqymzjAyQwSYCBTGJzsCYgp-VDZBbgSAYBIAA0wABaTAABISTsnolWHLKcrEhIywK7LTIUvzLJebpRWS8STTyXKeASZ4UlmNgBIGfiJNY4BgEwOBMCIKh3M0zBmEMHR6BVdCAGtcn69h4EuMN+vIDaEmtCoeCII0FhoTZXFCxBXGARg+R4YAOC2fRkDm4By2ABREBQchaQSNh4H4GgAGIATSwg0uQYMz0QNKXre2lICAA)

- Union Type으로 정의된 Person 타입을 갖는 person에서 공통 속성에 접근하지 않았을 때 발생하는 에러를 해결하는 문제이다.
- 타입을 좁혀야 한다.
- JavaScript 연산자 `in`을 사용해 객체에 특정 이름을 갖는 속성이 있는지 확인한다.

<br />

## 4번

> Type Predicates(타입 명제) 하는 문제

### 문제

```ts
/*

Intro:

    As we introduced "type" to both User and Admin
    it's now easier to distinguish between them.
    Once object type checking logic was extracted
    into separate functions isUser and isAdmin -
    logPerson function got new type errors.

Exercise:

    Figure out how to help TypeScript understand types in
    this situation and apply necessary fixes.

*/

interface User {
  type: "user";
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  type: "admin";
  name: string;
  age: number;
  role: string;
}

export type Person = User | Admin;

export const persons: Person[] = [
  {type: "user", name: "Max Mustermann", age: 25, occupation: "Chimney sweep"},
  {type: "admin", name: "Jane Doe", age: 32, role: "Administrator"},
  {type: "user", name: "Kate Müller", age: 23, occupation: "Astronaut"},
  {type: "admin", name: "Bruce Willis", age: 64, role: "World saver"},
];

export function isAdmin(person: Person) {
  return person.type === "admin";
}

export function isUser(person: Person) {
  return person.type === "user";
}

export function logPerson(person: Person) {
  let additionalInformation: string = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  console.log(` - ${person.name}, ${person.age}, ${additionalInformation}`);
}

console.log("Admins:");
persons.filter(isAdmin).forEach(logPerson);

console.log();

console.log("Users:");
persons.filter(isUser).forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates
```

### 풀이

```ts
interface User {
  type: "user";
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  type: "admin";
  name: string;
  age: number;
  role: string;
}

export type Person = User | Admin;

export const persons: Person[] = [
  {type: "user", name: "Max Mustermann", age: 25, occupation: "Chimney sweep"},
  {type: "admin", name: "Jane Doe", age: 32, role: "Administrator"},
  {type: "user", name: "Kate Müller", age: 23, occupation: "Astronaut"},
  {type: "admin", name: "Bruce Willis", age: 64, role: "World saver"},
];

export function isAdmin(person: Person): person is Admin {
  return person.type === "admin";
}

export function isUser(person: Person): person is User {
  return person.type === "user";
}

export function logPerson(person: Person) {
  let additionalInformation: string = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  console.log(` - ${person.name}, ${person.age}, ${additionalInformation}`);
}

console.log("Admins:");
persons.filter(isAdmin).forEach(logPerson);

console.log();

console.log("Users:");
persons.filter(isUser).forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/PQKgsAUJCSB2AuAnA9gLkpABNzBBAzpgO4CmmAlgigCYCuAxidZgETwCeADiS5vMpgBGyeAAtMAVXwlEmAIaxmuagFtKWHOXgByQrGRFMJOfnIy+A6uXzxKAc1rXxgkvFIlYfUSRUA6DdgA8rCMmMiCAFYk9PB8XGT03vQA1vaYADbIduT0xCZGAB5IcjFMARQIAtKccohy8GQAZrQhtsiwhNZS5grM1spqngC05Zl2AAoy+O2Yza3kM3YimLAkhhzcRogoiPj+UBAAogUy9NYk6Ac4mABi5A6IZMi0saIGFpje6ZyYACrxAGV6IhyJxYi1qFN4L04txOrBymJrJhTPBaPUFp4YXJOJx0uwVtESPh8LUCY1yCc9hgICBgDTKA1EI0SmRurIAN6I+KoTDaWjSRDaADc5VgchUFxRSHsoog1zkdilsFoKhciDl12Q9HotBqbVgvJsINgdjlAF8GQgZCzQgNKJgufKcBspdo5KpKCKxRKpcbZeVFcrVerNTgUOk-TLTRaaSQCpxkIhYq7MJNdjMALySQWYAA+eE9sDlkHjieTmHo7RsmG4GY6vPT01gAG0ALqYbMt8oc2FugUybQAGhWvt52gAsnICpgJwKmSoFLBh-IlbyAEwAVhH2t1+sx44AwqJyCpVgT8O5ONpMOahz2++OPYMV+LJeOAFIKMgAEWQJBXINeQAZnXEcIzde1YGsYp+CFW972dbBe1dccByFEc3zdABpeoyAnAAf9JIww1cpXXYCdx1PUMXaccCCQdo5BeG87wfVC+WfL1MLHPkACFEAYMgAHVyGI6xALXTAADYABZwOQSNx2EpN0mYUkADdB1vSA2xLCAyyTWI5hiTEKHwKCAAo62bRspnaABKXkbJmZEoMdcpHjRRBPBc2BfFTTMgs4otvQgS0DkMisTINcz2Ws+zDTTRKnNrRLzJzcwnWuLzaB8tL6wC+JO2C-lBTCiLSwTIzZhaUyZjGJt2gS+s7PrByPKQjJXHkagrANOR0jgRok0XA0jWjOxOz5MLrnIRpMEs-oixa5sHI67LrhwD1+sxQbhtG2jPGzPzfAgsNsAiuaFqW-B4r89bOq27a+q0PahtgEbEDGsyTsS3xdxog0Lp0rqqw6RSSF8MZLIAA0wIZMAAEg5U6sLvZHUf+oMMZRna3qYj6vp+9pzVhhzYwOcHpkjaGsks7QoPwVBtApyA-L2Cl0iZW6oIc3wvsOEpREsxqUv06nIbpuxLLZqnqylmHtHZZnWblDmBbEnmukFfnBeF0Wsia2A5cgYBgEwOBKxMMh5swdhnnkR5pQYZJLnNz54HgThmfNoh-aKuFgVBeB0gUOwAcQOxgGobV8GAURemEZBkmAddgHFbYDHsXxRHgFR0gAYgFewhldIZOEeKx6Dw-BICAA)

- 객체의 타입을 체크하는 로직(타입 가드 로직)을 함수로 분리했다.
- `parameterName is Type`을 작성해 함수에 전달된 매개변수의 명제를 만든다.
- 리턴 시에 명제를 만족할 조건을 반환하며 타입 가드 함수를 정의할 수 있다.
- 조건을 만족하면 true를 반환하고, 통과한 값은 명제를 만족하여 해당 타입을 갖는다.
