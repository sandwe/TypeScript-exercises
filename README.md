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

<br />

## 5번

> Utility Type을 사용해 타입 정의하는 문제

### 문제

```ts
/*

Intro:

    Time to filter the data! In order to be flexible
    we filter users using a number of criteria and
    return only those matching all of the criteria.
    We don't need Admins yet, we only filter Users.

Exercise:

    Without duplicating type structures, modify
    filterUsers function definition so that we can
    pass only those criteria which are needed,
    and not the whole User information as it is
    required now according to typing.

Higher difficulty bonus exercise:

    Exclude "type" from filter criterias.

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
  {
    type: "admin",
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    type: "user",
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    type: "admin",
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
  {
    type: "user",
    name: "Wilson",
    age: 23,
    occupation: "Ball",
  },
  {
    type: "admin",
    name: "Agent Smith",
    age: 23,
    role: "Administrator",
  },
];

export const isAdmin = (person: Person): person is Admin => person.type === "admin";
export const isUser = (person: Person): person is User => person.type === "user";

export function logPerson(person: Person) {
  let additionalInformation = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  console.log(` - ${person.name}, ${person.age}, ${additionalInformation}`);
}

export function filterUsers(persons: Person[], criteria: User): User[] {
  return persons.filter(isUser).filter((user) => {
    const criteriaKeys = Object.keys(criteria) as (keyof User)[];
    return criteriaKeys.every((fieldName) => {
      return user[fieldName] === criteria[fieldName];
    });
  });
}

console.log("Users of age 23:");

filterUsers(persons, {
  age: 23,
}).forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/utility-types.html
// https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#predefined-conditional-types
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
  {
    type: "admin",
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    type: "user",
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    type: "admin",
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
  {
    type: "user",
    name: "Wilson",
    age: 23,
    occupation: "Ball",
  },
  {
    type: "admin",
    name: "Agent Smith",
    age: 23,
    role: "Administrator",
  },
];

export const isAdmin = (person: Person): person is Admin => person.type === "admin";
export const isUser = (person: Person): person is User => person.type === "user";

export function logPerson(person: Person) {
  let additionalInformation = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  console.log(` - ${person.name}, ${person.age}, ${additionalInformation}`);
}

export function filterUsers(persons: Person[], criteria: Partial<Omit<User, "type">>): User[] {
  return persons.filter(isUser).filter((user) => {
    const criteriaKeys = Object.keys(criteria) as (keyof Partial<Omit<User, "type">>)[];
    return criteriaKeys.every((fieldName) => {
      return user[fieldName] === criteria[fieldName];
    });
  });
}

console.log("Users of age 23:");

filterUsers(persons, {
  age: 23,
}).forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/utility-types.html
// https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#predefined-conditional-types
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/PQKgsAUJCSB2AuAnA9gLkpABNzAVAlgLYCmm8ymAZvgDbzGJkAWpAJgIbzsCEmcmyRKwZkKAI1KUaxAB74x0rDgDuk2vUYBXAM4NtmHflgBzTO0yxNhCY2SVMAY0T4N+c+1isl2RMXibEWAFYGgBPZmRdTEJOByYjU3YaGgF7eBZHZ1d2ADpvTAB1NmRYAHJ4C2JiVkwAQVZCI31QvwAaTFVgsKp1EQBVXURtPKgIAFEZBgd8XXRRnEKXJmRNCtZNAAcafAdOBLJQjdJtJE0Hf19tdsJkVnxKUPzqOgYBvSpNWHP8EsxhalgLh+QW0FHSnA6pF2sHyG3Y2n0JW66UiUKyDDcHXicTMvkq1WqrXyHhqsGQFXSpGUy2kmDejCMlEEMXgwLM+hcmBm+V8AEdNPhfKTkMozA4HII7iZRAcNgkRpAABL4YwsRh3SjUByaOjhMQlHSYWRTGbEOb5CYOGiaYSYABE8EOxDtVBQhB6L0YThcGPhCogIGAGAgRg0lHYDlI9MwAG98o6jqhMKUdAxSgBufKwdgkJMnZwmTMQBbsYxmixWGxFhbIcWbPYlPNIBJFgC+wdDDHDkbqDSMsfjTqTpXYfbK1Zw2dzmHzLeJZaTlmsDAnPmQ0ibBeMbeDsg2ggpTswAAU9L8ALx0waYAA+vcasCLkD3B8cJROmCOQ3fSdP39gADaAC6mCXgB+QxrK5YpoMpTtFO0EALLsDImCIToGgxLAZTtKW5YAEwAKztLW2pwqyjbJgAwvEhCwMQ4TaKoxAbKUmCtkSxY4HGXELNgCbQaOD5wfkCwIcOABSHikAAIsgxAibxfF4UmADM+GcXxOAoBuyb1A+MxIJwgilPkHEQaJOACcOqaIIpWnYOJyYANKcKQiEAD-JGmmkOSpmD4apvlaaR9YUbAw61PmJTsKsplKeZSk8Q5UHDkJRj2Q5TmlAAQogZykAUtDbNomVaf5ABsAAswV8Tp0EFIINA1No7AAG5pmZtXJQ51nJrZZV8dlRU0KCOGWdg-mBbVNZ1uRwLDjlSQ0PFCyJQsPVaX1I5joNYk5tBtRlggmAAMqNOke04FNQUTZg9WRWOhmIMZdlmZAQFPhAL6IBUEqwB+Mz6f2l4ABRfmNv5nrAACUSYQ78Mz3iDAB8n7QzkAmgeel47cJRY-X974VDM0ZgwjEUntDcPo-+XL6GTaMU5jR447jA1fYTHxfOFmA0Mgxh-mN4PQ1D-4wwOSnSBUo53OFSRwEyiAsmyuMZvk9yYKDQNjiL4sS5tymsHLwIK7ASsqxetNjTk9WruxGv2Nr2j0nrY0wwbd2y0CMU0IrzINkEl7M6F80lPb7ZKf9oLSDk-PGKDAAGmAALSYAAJDGzMIRxGdZxjeG55n3vy375sB+FraJzDO6jFzlCfN8vzPBo9LaG7P5U-+wHtN62S-uwv1uDQAA8ADyF0j-S7TlE6pQoyjNP0sBksLL4FxBBTwwtwwzv0jDOQ74goOg7ZEvnmjhsLNHf3os47DOQx+iXmPYgAFbEOcOQANZP6Dfe+glvCLWv9Qh2BPIPVkSRx6T2nsmAS89F7AXtmvPwAQggAPvo-UIwxiAdUQKEE+1BiDNQAHIHXPpfO6qCN4GEGABYhZCDogTZpkH098GH4BIawchJBPp3VbDXMyQiICR0gNHdcxA44C1BqUNuqQzBlgCqpVApQRGQCPm3UGsJoZXAskpEsC5lHvQgAfJWYwIxMFBvHIWJR1EQGAMAPgGD4SkE1mAzQuJjj+AcN-OYjjMBMHgPADY2hUCOOUJElmRxtDeg2PAGgHhjA5EEMYYArBazaGAEwEk+pkDf2AKsWgLhQgpwEsMIJhAaCQACUEkJYSIlRPKXEhJSSUmIDSRkhwWScmeDyQU3w0hXEpzJPQLJzTnDxJTvhFOAAOHIlSaAAGINhCmIACaoKd-om19mUp02hIBAA)

- filterUsers 함수의 두번째 매개변수의 타입을 정의해야 한다.
- `criteria`는 User의 `name`, `age`, `occupation` 속성들로 이루어진다.
- 따라서, `Partial<Type>` Utility Type을 사용해 특정 타입의 부분 집합으로 이루어진 타입을 정의한다.
- User의 `type` 속성은 `criteria`를 정의할 때 제외되어야 한다.
- `type` 속성만 제거하기 위해서 `Omit` Utility Type을 사용한다.
- `Omit<Type, Keys>`: 특정 객체 타입에서 Keys로 명시한 프로퍼티를 제거해 새로운 타입을 구성한다.

<br/>

## 6번

> Function Overloads 사용하는 문제

### 문제

```ts
/*

Intro:

    Filtering requirements have grown. We need to be
    able to filter any kind of Persons.

Exercise:

    Fix typing for the filterPersons so that it can filter users
    and return User[] when personType='user' and return Admin[]
    when personType='admin'. Also filterPersons should accept
    partial User/Admin type according to the personType.
    `criteria` argument should behave according to the
    `personType` argument value. `type` field is not allowed in
    the `criteria` field.

Higher difficulty bonus exercise:

    Implement a function `getObjectKeys()` which returns more
    convenient result for any argument given, so that you don't
    need to cast it.

    let criteriaKeys = Object.keys(criteria) as (keyof User)[];
    -->
    let criteriaKeys = getObjectKeys(criteria);

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
  {type: "user", name: "Wilson", age: 23, occupation: "Ball"},
  {type: "admin", name: "Agent Smith", age: 23, role: "Anti-virus engineer"},
];

export function logPerson(person: Person) {
  console.log(` - ${person.name}, ${person.age}, ${person.type === "admin" ? person.role : person.occupation}`);
}

export function filterPersons(persons: Person[], personType: string, criteria: unknown): unknown[] {
  return persons
    .filter((person) => person.type === personType)
    .filter((person) => {
      let criteriaKeys = Object.keys(criteria) as (keyof Person)[];
      return criteriaKeys.every((fieldName) => {
        return person[fieldName] === criteria[fieldName];
      });
    });
}

export const usersOfAge23 = filterPersons(persons, "user", {age: 23});
export const adminsOfAge23 = filterPersons(persons, "admin", {age: 23});

console.log("Users of age 23:");
usersOfAge23.forEach(logPerson);

console.log();

console.log("Admins of age 23:");
adminsOfAge23.forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/functions.html#function-overloads
```

### 풀이

```ts
/*

Intro:

    Filtering requirements have grown. We need to be
    able to filter any kind of Persons.

Exercise:

    Fix typing for the filterPersons so that it can filter users
    and return User[] when personType='user' and return Admin[]
    when personType='admin'. Also filterPersons should accept
    partial User/Admin type according to the personType.
    `criteria` argument should behave according to the
    `personType` argument value. `type` field is not allowed in
    the `criteria` field.

Higher difficulty bonus exercise:

    Implement a function `getObjectKeys()` which returns more
    convenient result for any argument given, so that you don't
    need to cast it.

    let criteriaKeys = Object.keys(criteria) as (keyof User)[];
    -->
    let criteriaKeys = getObjectKeys(criteria);

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
  {type: "user", name: "Wilson", age: 23, occupation: "Ball"},
  {type: "admin", name: "Agent Smith", age: 23, role: "Anti-virus engineer"},
];

export function logPerson(person: Person) {
  console.log(` - ${person.name}, ${person.age}, ${person.type === "admin" ? person.role : person.occupation}`);
}

export const getObjectKeys = <T>(obj: T) => Object.keys(obj) as (keyof T)[];

// overload signature (선언)
export function filterPersons(persons: Person[], personType: "user", criteria: Partial<Omit<User, "type">>): User[];
export function filterPersons(persons: Person[], personType: "admin", criteria: Partial<Omit<Admin, "type">>): Admin[];
// implementation signature (구현)
export function filterPersons(persons: Person[], personType: string, criteria: Partial<Person>): Person[] {
  return persons
    .filter((person) => person.type === personType)
    .filter((person) => {
      let criteriaKeys = getObjectKeys(criteria);
      return criteriaKeys.every((fieldName) => {
        return person[fieldName] === criteria[fieldName];
      });
    });
}

export const usersOfAge23 = filterPersons(persons, "user", {age: 23});
export const adminsOfAge23 = filterPersons(persons, "admin", {age: 23});

console.log("Users of age 23:");
usersOfAge23.forEach(logPerson);

console.log();

console.log("Admins of age 23:");
adminsOfAge23.forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/functions.html#function-overloads
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/PQKgsAUJCSB2AuAnA9gLkpABNzAVAlgLYCmm8ymAZvgDbzGJkAWpAJgIbzsCEmcmyRKwZkKAI1KUaxAB74x0rDgDuk2vUYBXAM4NtmHflgBzTO0yxNhCY2SVMAY0T4N+c+1isl2RMXibEWAFYGgBPZmRdTEJOByYjU3YaGgF7eBZHZ1d2ADpvTAB1NmRYAHJ4C2JiVkwAQVZCI31QvwAaTFVgsKp1EQBVXURtPKgIAFEZBgd8XXRRnEKXJmRNCtZNAAcafAdOBLJQjdJtJE0Hf19tdsJkVnxKUPzqOgYBvSpNWHP8EsxhalgLh+QW0FHSnA6pF2sHyG3Y2n0JW66UiUKyDDcHXicTMvkq1WqrXyHhqsGQFXSpGUy2kmDejCMlEEMXgwLM+hcmBm+V8AEdNPhfKTkMozA4HII7iZRAcNgkRpAABL4YwsRh3SjUByaOjhMQlHSYWRTGbEOb5CYOGiaYSYABE8EOxDtVBQhB6L0YThcGPhCogIGAGAgRg0lHYDlI9MwAG98o6jqhMKUdAxSgBufKwdgkJMnZwmTMQBbsYxmixWGxFhbIcWbPYlPNIBJFgC+wdDDHDkbqDSMsfjTqTpXYfbK1Zw2dzmHzLeJZaTlmsDAnPmQ0ibBeMbeDsg2ggpTswAAU9L8ALx0waYAA+vcasCLkD3B8cJROmCOQ3fSdP39gADaAC6mCXgB+QxrK5YpoMpTtFO0EALLsDImCIToGgxLAZTtKW5YAEwAKztLW2pwqyjbJgAwvEhCwMQ4TaKoxAbKUmCtkSxY4HGXELNgCbQaOD5wfkCwIcOABSHikAAIsgxAibxfF4UmADM+GcXxOAoBuyb1A+MxIJwgilPkHEQaJOACcOqaIIpWnYOJyYANKcKQiEAD-JGmmkOSpmD4apvlaaR9YUbAw61PmJTsKsplKeZSk8Q5UHDkJRj2Q5TmlAAQogZykAUtDbNomVaf5ABsAAswV8Tp0EFIINA1No7AAG5pmZtXJQ51nJrZZV8dlRU0KCOGWdg-mBbVNZ1uRwLDjlSQ0PFCyJQsPVaX1I5joNYk5tBtRlggmAAMqNOke04FNQUTZg9WRWOhmIMZdlmZAQFPhAL6IBUEqwB+Mz6f2l4ABRfmNv5nrAACUSYQ78Mz3iDAB8n7QzkAmgeel47cJRY-X974VDM0ZgwjEUntDcPo-+XL6GTaMU5jR447jA1fYTHxfOFmA0Mgxh-mN4PQ1D-4wwOSnSBUo53OFSRwEyiAsmyuMZvk9yYKDQNjiL4sS5tymsHLwIK7ASsqxetNjTk9WruxGv2Nr2j0nrY0wwbd2y0CMU0IrzINkEl7M6F80lPb7ZKf9oLSDk-PGKDAAGmAALSYAAJDGzMIRxGdZxjeG55n3vy375sB+FraJzDO6jFzlCfN8vzPBo9LaG7P5U-+wHtN62S-uwv1uDQAA8ADyF0j-S7TlE6pQoyjNP0sBksLL4FxBBTwwtwwzv0jDOQ74goOg7ZEvnmjhsLNHf3os47DOQx+iXmPYgAFbEOcOQANZP6Dfe+glvCLWv9Qh2BPIPVkSRx6T2nsmAS89F7AXtmvPwAQggAPvo-UIwxiAdUQKEE+1BiDNQAHIHXPpfO6qCN4GEGABYhZCDogTZpkH098GH4BIawchJBPp3VbDXMyQiICR0gNHdcxA44C1BqUNuqQzBlgCqpVApQRGQCPm3UGsJoZXAskpEsC5lHvQgAfJWYwIxMFBvHIWJR1EQGAMAPgGD4SkE1mAzQuJjj+AcN-OYjjMBMHgPADY2hUCOOUJElmRxtDeg2PAGgHhjA5EEMYYArBazaGAEwEk+pkDf2AKsWgLhQgpwEsMIJhAaCQACUEkJYSIlRPKXEhJSSUmIDSRkhwWScmeDyQU3w0hXEpzJPQLJzTnDxJTvhFOAAOHIlSaAAGINhCmIACaoKd-om19mUp02hIBAA)

- function overloading(함수 오버로딩): 같은 이름을 갖는 함수지만 매개변수 갯수나 타입을 다르게 정의할 수 있다.
- 함수의 로직은 같지만 `personType`에 따라 User 또는 Admin을 필터링할 수 있도록 해야 하기 때문에 함수 오버로딩을 사용할 수 있다.

<br />

## 7번

> Generic 사용하는 문제

### 문제

```ts
/*

Intro:

    Filtering was completely removed from the project.
    It turned out that this feature was just not needed
    for the end-user and we spent a lot of time just because
    our office manager told us to do so. Next time we should
    instead listen to the product management.

    Anyway we have a new plan. CEO's friend Nick told us
    that if we randomly swap user names from time to time
    in the community, it would be very funny and the project
    would definitely succeed!

Exercise:

    Implement swap which receives 2 persons and returns them in
    the reverse order. The function itself is already
    there, actually. We just need to provide it with proper types.
    Also this function shouldn't necessarily be limited to just
    Person types, lets type it so that it works with any two types
    specified.

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

function logUser(user: User) {
  const pos = users.indexOf(user) + 1;
  console.log(` - #${pos} User: ${user.name}, ${user.age}, ${user.occupation}`);
}

function logAdmin(admin: Admin) {
  const pos = admins.indexOf(admin) + 1;
  console.log(` - #${pos} Admin: ${admin.name}, ${admin.age}, ${admin.role}`);
}

const admins: Admin[] = [
  {
    type: "admin",
    name: "Will Bruces",
    age: 30,
    role: "Overseer",
  },
  {
    type: "admin",
    name: "Steve",
    age: 40,
    role: "Steve",
  },
];

const users: User[] = [
  {
    type: "user",
    name: "Moses",
    age: 70,
    occupation: "Desert guide",
  },
  {
    type: "user",
    name: "Superman",
    age: 28,
    occupation: "Ordinary person",
  },
];

export function swap(v1, v2) {
  return [v2, v1];
}

function test1() {
  console.log("test1:");
  const [secondUser, firstAdmin] = swap(admins[0], users[1]);
  logUser(secondUser);
  logAdmin(firstAdmin);
}

function test2() {
  console.log("test2:");
  const [secondAdmin, firstUser] = swap(users[0], admins[1]);
  logAdmin(secondAdmin);
  logUser(firstUser);
}

function test3() {
  console.log("test3:");
  const [secondUser, firstUser] = swap(users[0], users[1]);
  logUser(secondUser);
  logUser(firstUser);
}

function test4() {
  console.log("test4:");
  const [firstAdmin, secondAdmin] = swap(admins[1], admins[0]);
  logAdmin(firstAdmin);
  logAdmin(secondAdmin);
}

function test5() {
  console.log("test5:");
  const [stringValue, numericValue] = swap(123, "Hello World");
  console.log(` - String: ${stringValue}`);
  console.log(` - Numeric: ${numericValue}`);
}

[test1, test2, test3, test4, test5].forEach((test) => test());

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
// https://www.typescriptlang.org/docs/handbook/2/generics.html
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

function logUser(user: User) {
  const pos = users.indexOf(user) + 1;
  console.log(` - #${pos} User: ${user.name}, ${user.age}, ${user.occupation}`);
}

function logAdmin(admin: Admin) {
  const pos = admins.indexOf(admin) + 1;
  console.log(` - #${pos} Admin: ${admin.name}, ${admin.age}, ${admin.role}`);
}

const admins: Admin[] = [
  {
    type: "admin",
    name: "Will Bruces",
    age: 30,
    role: "Overseer",
  },
  {
    type: "admin",
    name: "Steve",
    age: 40,
    role: "Steve",
  },
];

const users: User[] = [
  {
    type: "user",
    name: "Moses",
    age: 70,
    occupation: "Desert guide",
  },
  {
    type: "user",
    name: "Superman",
    age: 28,
    occupation: "Ordinary person",
  },
];

// Generic 함수
export function swap<T, U>(v1: T, v2: U): [U, T] {
  return [v2, v1];
}

function test1() {
  console.log("test1:");
  const [secondUser, firstAdmin] = swap(admins[0], users[1]);
  logUser(secondUser);
  logAdmin(firstAdmin);
}

function test2() {
  console.log("test2:");
  const [secondAdmin, firstUser] = swap(users[0], admins[1]);
  logAdmin(secondAdmin);
  logUser(firstUser);
}

function test3() {
  console.log("test3:");
  const [secondUser, firstUser] = swap(users[0], users[1]);
  logUser(secondUser);
  logUser(firstUser);
}

function test4() {
  console.log("test4:");
  const [firstAdmin, secondAdmin] = swap(admins[1], admins[0]);
  logAdmin(firstAdmin);
  logAdmin(secondAdmin);
}

function test5() {
  console.log("test5:");
  const [stringValue, numericValue] = swap(123, "Hello World");
  console.log(` - String: ${stringValue}`);
  console.log(` - Numeric: ${numericValue}`);
}

[test1, test2, test3, test4, test5].forEach((test) => test());

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
// https://www.typescriptlang.org/docs/handbook/2/generics.html
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/PQKgsAUJCSB2AuAnA9gLkpABNzAxAlgDbwCmi+sA5pgO4CGAzpgMbIC2ADoSaYQJ6ZEJNsgBuJACaYAZijaZ4ACxKYOKAFYlm8AHRYc0eAoCuiWJMzJjRpXRuL8TaSTumV9JuuMMjsZL5JJSX1saWREBWVMElgJAFpvMkw6WNoVBg4YozpMQn9LaQV8NhUvH0wAIy06RJDLUwLpfGYVNhS6SiT4ZEIpbwVkTAlBhmQdTAA5EgAPG2L3dMUrXrqKHxcpQkdSWAHIlTVkCWNtTDbYDuEsvSgIHEwAQVg+egEaFUU6cWTMcxpVQgpcYAYQAogB5ADkTnIMSkE2aAGsBr1MN46rYjPhCu9BClhmx+JgGPQOGiGEkLiUYewiiU9vB5qtdkoVKw2GxjLB8PA+AAaTA82jLKRVTDiRACaRc57JVKs1QaLTwOo0EVDEhNbm8AQME4tSQAQgwEFB0zIzEcJHQt3u0E43BKCGJpNoDmYikEWhI+HETAATKoyKNYEx8V74KZQ-t5BQMVEhBKKZZEBIyOMACpRaWwbT4ZC7HkUwiFRzJQhCOgSPjxsgkAV0bTGOiEfjjADqpW8AQs3UVYnwacFRhoPM9h0yEV5mQYN3uD0Io0iZZzeYLxKWxl6sEhARaDAYdHIRLFWzYPN7gzKKruOAACsH19OSAwBdx4Exn8PiYNMd+1YgiJMKOShygI8BqgofAznUGRaNi+CSDckAgMAJoUKQiDSI2KgAKoUhEADeGLQdamCQokiCQgA3HUVJkT45BULRt7YJcqC-MYbBVIgLH3MgzDMMYHB2PmsAcYxFCUCxAC+6EIGQ2EtI8EjnrsxGsVBmQcZCVZqTRdF0CUElIFJfE4OxnHcWQ5nYCg3AmUx0mQHJtyroy655JQ+FkAAFJRHE+YgACUmAafcrChkYHDIEwAC85LBjoFBptM4LSP5BGhQA1JgACMtksAWozcDoXm+QABpgcSYAAxAAJIRMUMDJmBBRxjWUTo9EyQKnUEToly9Zg-XpgJQkiR5sAyRVwWySa7libkyCUA8qkUL5ekUBxa1qaF4U4JF5TNZgCVbaGyWxDM6WbetsA5flhVHT0JBlStlXVXVjXNa1u3bSNhHnd1RkkMNjVA0NfWA3dOj2aDs3zbcR3ZHdDA7XdADaAC6p2YBjdQHfc2DPjp52QnydT3PROntkQhCYAAQogJwvuTlMWZ0HEAMwAAwU5p9xwzp4JJoEVF1L1BPs8TpGk3dbMCzg1PkQAyqQ4gK0THNkQALHz0uCC9OlqyQGsS5AWMsZAyOJYgaNtQR2O4-jmmE0TJPkZRmta78IM6QAsrFrP8z7ySc5gADs+uK9g43CaJBY6QAIi+ZBGJQxiDiQkISyHOBu-cHsUQR3ta8rkIq8JZDnKXROWf6AAceda3Hk1icLqYUEeAiTiGOeaa5lsmjMMWIEYi3riSdAcAAPBmAq4QAfL5oh5Rx8-iv6gXBRxGO4QKGY427QiRmYeOiP6Aqr0PECuZAE8si+8B5b5+11M9pXlbuT9r5Cc3v8VIwGMKSRQkEFAUTQ7bwD+rAHGCUp4cFumpBgGMeZYwFJRFBeUsb-00l5IKvkQEFjAVlQqXkYG+UgT4GBuC74QAfgoJ+-pX5hQAaGF6b1KC+W-j4Lef8nqALxkQ2IMCIH4CgUFOBLpp6ZWDKg9ByRUYY2wbg+45C7qEK0MQmhZCVoEKofAIKtCFpcjXI-HwXMWFuw-q9L+pALGoH4Ww8owCtGxHATIcRPhJG4wQbIu28iMEESwTg3R3kCKaNAUYsJ+ivGGNIS5ExuYpqMJ8DrKxziOF2KfjrRxqjDqCIxgY0RxI3ESBgVIvx50QkNiUWg-J2B1FqUoXEnRdQmkbWEeUu6xi3KmJSfY+AABWDJmkbGcO4YMoZeSBFRSEaZKgAA1Fsxh6xWTIM0ZZhBVmVNJL5PK-ouYCkhAACRIK2QY7Zwi9CcWM4qWT3pVRqmrJyHVCKSSWSs+GDSirsM-o8z6EwuIbOYG82AwLyDMC2asmavTIAY0GXlAUgzL6pPgEctFOtkVPyGVjHQYRECgkbIoXyvlBmhTiovNFr9cGQGAMATAcAWCMBUNiTAfArDJCEMSSMzBEQ2npZgRQ8B4AcDRvSmgkqdDPgYMwcgHB4CAioDocIlBgDDGYAwYAnxYgVGQMgREwB-TAFNmQPgEg6B8DiDKnQwrCR0oZcK0V4rgCSpoNK0isr5WKpSJQFViA1Uaq1TqiQeqDVGuAJ0cwkLZx2sIJAIAA)

- 문제에 `swap`함수의 매개변수는 Person 타입에 존재하는 값만으로 제한하지 않는다고 명시되어 있다.
- 따라서, 어떤 타입이든 매개변수로 전달될 수 있어야 한다.
- Generic을 사용하면 매개변수로 타입을 넘겨주는 것처럼 동작한다.

<br />

## 8번

> Intersection type 사용하는 문제

### 문제

```ts
/*

Intro:

    Project grew and we ended up in a situation with
    some users starting to have more influence.
    Therefore, we decided to create a new person type
    called PowerUser which is supposed to combine
    everything User and Admin have.

Exercise:

    Define type PowerUser which should have all fields
    from both User and Admin (except for type),
    and also have type 'powerUser' without duplicating
    all the fields in the code.

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

type PowerUser = unknown;

export type Person = User | Admin | PowerUser;

export const persons: Person[] = [
  {type: "user", name: "Max Mustermann", age: 25, occupation: "Chimney sweep"},
  {type: "admin", name: "Jane Doe", age: 32, role: "Administrator"},
  {type: "user", name: "Kate Müller", age: 23, occupation: "Astronaut"},
  {type: "admin", name: "Bruce Willis", age: 64, role: "World saver"},
  {
    type: "powerUser",
    name: "Nikki Stone",
    age: 45,
    role: "Moderator",
    occupation: "Cat groomer",
  },
];

function isAdmin(person: Person): person is Admin {
  return person.type === "admin";
}

function isUser(person: Person): person is User {
  return person.type === "user";
}

function isPowerUser(person: Person): person is PowerUser {
  return person.type === "powerUser";
}

export function logPerson(person: Person) {
  let additionalInformation: string = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  if (isPowerUser(person)) {
    additionalInformation = `${person.role}, ${person.occupation}`;
  }
  console.log(`${person.name}, ${person.age}, ${additionalInformation}`);
}

console.log("Admins:");
persons.filter(isAdmin).forEach(logPerson);

console.log();

console.log("Users:");
persons.filter(isUser).forEach(logPerson);

console.log();

console.log("Power users:");
persons.filter(isPowerUser).forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/utility-types.html
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

type PowerUser = Omit<User, "type"> & Omit<Admin, "type"> & {type: "powerUser"};

export type Person = User | Admin | PowerUser;

export const persons: Person[] = [
  {type: "user", name: "Max Mustermann", age: 25, occupation: "Chimney sweep"},
  {type: "admin", name: "Jane Doe", age: 32, role: "Administrator"},
  {type: "user", name: "Kate Müller", age: 23, occupation: "Astronaut"},
  {type: "admin", name: "Bruce Willis", age: 64, role: "World saver"},
  {
    type: "powerUser",
    name: "Nikki Stone",
    age: 45,
    role: "Moderator",
    occupation: "Cat groomer",
  },
];

function isAdmin(person: Person): person is Admin {
  return person.type === "admin";
}

function isUser(person: Person): person is User {
  return person.type === "user";
}

function isPowerUser(person: Person): person is PowerUser {
  return person.type === "powerUser";
}

export function logPerson(person: Person) {
  let additionalInformation: string = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  if (isPowerUser(person)) {
    additionalInformation = `${person.role}, ${person.occupation}`;
  }
  console.log(`${person.name}, ${person.age}, ${additionalInformation}`);
}

console.log("Admins:");
persons.filter(isAdmin).forEach(logPerson);

console.log();

console.log("Users:");
persons.filter(isUser).forEach(logPerson);

console.log();

console.log("Power users:");
persons.filter(isPowerUser).forEach(logPerson);

// In case if you are stuck:
// https://www.typescriptlang.org/docs/handbook/utility-types.html
```

[TypeScript Playground에서 코드 보기](https://www.typescriptlang.org/play?#code/PQKgsAUJCSB2AuAnA9gLkpABNzAFFAVgKYDG8mA5okQO6YCGsAJpjUZkc0SwK4AOmAJawGmAM6D4PevEHIRNSQAssOMcgC27HmKKIx4+PUSzYFTPGSYl9AG7sNyakNgAzADY9OJIgDpV2AAqSnpErk5EADSs7EykgnEslpgk1DLs9JiwtJh8euoi8ACeeQEp9O7u3HjIbIgAqrqIrEqCJEpCBmL8fMi6SVYkmgBGwkRlRPaIRfCtZpiNegzMmACCTBrC1nZ+GBAAogAeeiSCuuhQEDiYACJhYxYl7Li1eovNNK3t4krIPO4sGz2BiVTCuQREAFiMquFAaTDDZCzBZNZYsdabEQACiIhx8fHI4WaxTyAEpImVGCwKuptsCSewAOS9OrvRmsZR-chMfjuNoyYQUSmg2bscGQpgGLailLIOL+S4gYB7YTwPSueg+FFLADeZQZqEwjJ0ekZAG4yrB6FpDWIkIKLVccPQKERDbAeBphnpHddkCQSPwBfJbfazI6AL4qhDqzXsDFbPVO7AGo30DbCc2W61uwyIB2U13uz3exC+nAoKqh-PhyBRy4Mmqs1EAXkwAHlNvAADzvaIAIgZ-YAfJgAGQdrvdhOwAdD0cTnWp-sst5NfsRx2QXG9EyPPJ4fLyTBt96YAA+awzIkvL2bPr2O6c5CGsDtuSPb8NuE-AG0ALonpgv5lDq+65saTSMtEVo2kaACy9CHJg8E6GqiAaIwsDQQwRaYAATAArNE-qBnwwawIajIAMKtBo2RFOIbBEHw7IRhSyaYGBqaMummI4bBEEAFKMOwNzIEQOEurmADM+HRJWEEzmcSAyE4bEcdc3FPFRJqIAJOZUQA0ukKEAD+VKa0TSYa+EySRAZBrIIZGqsdooFaPDwBpoHgVRfGZjBhlGgAQogPBagA6oIlRnFJeEAGwACwKcgVZGpFTgAuIOz6Zg7GgWU1w8auDRQZp1w4IJVEAHKCAA1vVgiYAAypY2TQUVzp4UlxFddgilUfBcp6Gp+kVZVmCkU5ciUUa1EyJQKCaKaZT1v+W4QK4PCwGQs2dDOWJ5PoLk-idsCkoax0FJ0V6YlxZTUFIiAiNd8i+I2LZfWm15ZhA9aQNtu3OSIZzvEdn7fp+l0fudt1nkm1xPTwL2wwUH1PCe32QaakZ7EDe3Hmcd5rnoEPnVD50w29oMGCTZW6o9RDPa9n4YweX1tsyrwM-peOXE+e4EyDmDuMgFBnQU5MFJTBSkg9nFVOQ6ZMJIs0VHARKYSD1aCkBjJ-dcgiuJgWJnIdNOkvLiOTQwTCqyDGtuE42v7W2NO+Ip5bYPWRsm2bYjg5b1v9XbDvq+4msuxRQEe9N5Eg97+VlMbpvEzzQfQyHnHXCravyE7Wsx22AAGAAkOoe4p7GYBXceOQns0RiXSe+zgr7qFUvhixQWLl5XbOCTXdds9Jw86nnjuR87GEUc3pL85AHdpX4PdYoyM5iKgjIL5ANNiL44LuOhAczqSh9OPsmpKFiPeS-Iu+XMvXdr4-S-yJ3q-i+v7xbzvjr70PjFE+YMmjnyJFfdot9xb3wuptZ+X9e5vwgAg7u39GT00wHpP+j9AFHxAWIem7xwGX2vtAiW0NNrAGAJgOA5RdBCBNkUP4DBnB2givVC41DrDwHgHwLe1CaBCPZkQMQqRBAEncIwCgvgnAUGAEwf0YhgA2GYIiZA9VgBeRipIIoABaBkB8lDwA0O4SAQA)

- User와 Admin 타입 속성을 모두 갖고, type은 `powerUser`로 새로 정의되어야 한다.
- type은 새로 정의해줘야 하므로 User와 Admin의 `type` 속성을 제거한 새로운 타입을 intersection한다.
- 그리고 `{ type: 'powerUser' }`를 intersection한다.
