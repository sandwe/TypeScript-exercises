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
