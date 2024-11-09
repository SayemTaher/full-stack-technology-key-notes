
# Combined Documentation for TypeScript Files

This document contains combined information from two TypeScript files.

---

## File: objects.ts

```typescript
{
    //  base of oop 
    // -- inheritence
    // -- polymorphism
    // -- abstraction
    // -- encapsulation
    
    class Animal {
        // public name: string
        // public sound: string
        // public age: number 

        // parameter properties = no need to define types twice
        constructor(public name: string, public sound: string, public age: number) {
            // this.name = name;
            // this.sound = sound; 
            // this.age = age
        }

        makeSound() { // void function --> use normal function as this doesn't work for arrow functions
            console.log(`${this.name} says ${this.sound} and it is ${this.age} years old`);
        }
    }

    const createDog = new Animal("Dog", "Bau bau", 15)
    createDog.makeSound()
    const createCat = new Animal("Cat", "Meauw meauw", 2)
    createCat.makeSound()

    // inheritence 
    // ----------
    // ----------
    // inheritence

    class Person {

        constructor(public name: string, public age: number, public city: string) { }
        
        getPersonInfo() {
            console.log(`${this.name} is ${this.age} years old and he lives in ${this.city}`);
        }
    }

    class Student1 extends Person {

        constructor(public name:string, public age: number, public city : string, public nationality: string) {
            super(name,age,city) // here name,age,city is getting ionherited from the Person class
        }
        studyHours(numberOfStudyHours : number) {
            console.log(`Student  ${this.name} is from ${this.nationality} and he studies for  ${numberOfStudyHours} hours`);
        }
        studentWorking() {
            console.log(`i work as a student`);
        }
    }

    const studentsInsight = new Student1("Sayem", 24, "Eindhoven", "Bangladesh")
    studentsInsight.name = "Rafeq"
    studentsInsight.nationality = "Syria"
    studentsInsight.studyHours(25)
    studentsInsight.getPersonInfo()

    // instanceof type 

    const isStudent = (user: Person): user is Student1 => {
        return user instanceof Student1
    }

    const checkPersonData = (user: Person) => {
        if (isStudent(user)) {
           user.studentWorking() 
        }
    }
    const studentInstance = new Student1(
      "Sayem",
      24,
      "Eindhoven",
      "Bangladesh"
    );
    checkPersonData(studentInstance); 
    

//  in type guard 
    
    type NormlaUser = {
        name: string;
        
    }
    type AdminUser = {
        name: string
        role:string
    }
    const normalUser: NormlaUser = {
        name:"Normal User"
    }
    const adminUser: AdminUser = {
        name: "Admin user",
        role:"Admin"
    }

    const checkUser = (user: NormlaUser | AdminUser) => {
        if ('role' in user) {
            console.log(`You are logged in as an ${user.role}`)
        }
        else {
            console.log(`You're logged in as a normal user`);
        }
    }
    checkUser(normalUser)

    // typeof guard

    const chekTypeOf = (value1: string | number, value2: string | number): string | number  => {
        if (typeof value1 === "number" && typeof value2 === "number") {
          return value1 + value2;
        } else  {
            return value1.toString() + value2.toString();
        }
    }
    console.log(chekTypeOf(5, 5));

    // access modifiers 

    class BankAccount {
        public name : string
        public id : number
        protected _balance: number
        
        constructor(name: string, id: number, _balance: number) {
            this.name = name 
            this.id = id 
            this._balance = _balance
        }
        // public getBalance() {
        //     return this._balance
        // }
        // public addDeposit(amount: number) {
        //     this._balance += amount
        // }
        // getter
        get getBalance() {
            return this._balance
        }
        // setter 
        set deposit(amount: number) {
            this._balance += amount
        }
    }
    class StudentAccount extends BankAccount {
        public studentId: number 
        constructor(studentId: number, name: string, id: number, _balance: number) {
            super(name,id,_balance)
            this.studentId = studentId
        }
    }

    const createBankAccount = new BankAccount("Sayem Ibne Taher", 50567, 100)
    createBankAccount.deposit= 200
    
    console.log(createBankAccount.getBalance);

    // static and void in OOP

    class PremiumAccount{
        static count: number = 0 
        
        static increment() {
            return PremiumAccount.count ++
        }
        static decrement() {
            return PremiumAccount.count --
        }
    }

    console.log(PremiumAccount.increment());
    console.log(PremiumAccount.increment());
    console.log(PremiumAccount.increment());
    console.log(PremiumAccount.decrement());
    console.log(PremiumAccount.decrement());

    // Polymorphism

    class MainObject {

        getObj(): number {
            return 0
        }
    }

    class Object1 extends MainObject {
        radius: number 
        constructor(radius: number) {
            super()
            this.radius = radius
            
        }
        getObj(): number {
            return Math.PI * this.radius * this.radius
        }
    }

    const calculateRadius = (param: MainObject)=>{
        console.log(param.getObj());
    }

    const instance1 = new MainObject()
    const instance2 = new Object1(10)
    calculateRadius(instance2)

//  abstracation  ---> interface --< abstract
    
    interface Vehicle {
        startCar() : void;
        stopCar(): void;
        moveCar(): void;
    }
    class Car implements Vehicle {
        startCar(): void {
            console.log(`I am starting the car`);
        }
        stopCar(): void {
            console.log(`I am stopping the car`);
        }
        moveCar(): void {
            console.log(`I am moving the car`);
        }
    }

    const createCar1 = new Car()

    //  using abstract class 

    abstract class Car2{
        moveCar(): void {}
        startCar(): void {}
        stopCar(): void { }
        
        raceCar() {
            console.log(`We are racing now`);
        }
    }

    class Car3 extends Car2 {
        moveCar(): void {
            console.log(`I am moving the car`);
        }
        startCar(): void {
            console.log(`I am starting the car`);
        }
        stopCar(): void {
            console.log(`i am stopping the car`);
        }
    }

    const createCar3 = new Car3()
    
    // Encapsulation 

    
    
    
    
}
```

---

## File: index.ts

```typescript
{
    // basic data type

    //  primitive = string, number, boolean,null, undefined
    //  what is primitive? primitive values refers to basic data types that represent singe values and are not immutable.
    // meaning that their values cannot be changed once assigned and can not be referenced 

    let isRunning: boolean = false

    // undefined 

    let x: undefined = undefined

    // null 

    let y: null = null

    // if type is not defined it will be counted as any ( not recommended)


    // No-primitive - non primitive values are immutable and can be referenced also they hold multiple datas and can be chnaged after assigned

    let students: string[] = ['rafeq', 'saadi']

    //  tuple --> array -> ordered

    let coordinates: [number, string] = [20, 'Sayem']

    //reference type --> object

    const user: {
        readonly school: 'Fontys ICT' // literal type -- always fixed
        firstName: string;
        middleName?: string; // optional type
        lastName: string;

    } = {
        school: 'Fontys ICT',
        firstName: 'Sayem',
        lastName: 'Taher'
    }

    // Function 

    function add(num1: number, num2: number): number {
        return num1 + num2
    }

    // using function inside 

    const accountDetails: {
        name: string;
        balance: number;
        addBalance: Function;
    } = {
        name: 'Sayem Ibne Taher',
        balance: 0,
        addBalance(balance: number): string {
            return `Account balance is ${this.balance + balance}`
        }
    }

    // spread operator , rest operator and destructuring 
    
    // Spread operator 
    
    let groceries: string[] = ["orange", "apple"]
    let drinks: string[] = ["cola", "sprite"]
    
    groceries.push(...drinks)

    //with objects 
    let group1 = {
        name: "faysal ",
        age: 20,
        gender: "male"
    }
    let group2 = {
        name: "fahim ",
        age: 22,
        gender: "male",
    };

    let groups = {
        ...group1,
        ...group2
    }

    // rest operator 

    const friendList = (...friends: string[]) => { // spread operator creates a new array containing all the arguments 
        friends.forEach((friend: string) => console.log(`Hello ${friend}`));
            
    }



    // destructuirg 

    // for objects 
 
    const userInfo: {
        name: {firstName : string, lastName:string};
        age: number;
        dateOfBirth: string;
    } =
    {
        name: {
            firstName: "Sayem ",
            lastName : "Taher"
        },
        age: 10,
        dateOfBirth: 'September 6'
    }

    const { name : {firstName,lastName}, age, dateOfBirth : birthDate} = userInfo // here you can't assign type of the value instead it will act as alias

    // aray destructuring

    let friendsData : string[]= ["rafeq", 'niels', 'gijs', 'alex', 'rachel']
    
    let [, , , goodFriend, ...rest] = friendsData
    console.log(friendsData.length)


    // type alias 

    type Student = {
        name: string;
        id: number;
        address?: string;
        year: number;
    }
    
    let ictDepartemnt: Student = {
        name: "Sayem",
        id: 4669045,
        address: "Eindhoven",
        year : 2024
        
    }
    // string type 

    type UserName = string 

    let userName : UserName = "Sayem"
    
    // function type 

    type AddValue = (num1: number, num2: number) => number;

    const addValue : AddValue = (num1,num2) => num1 + num2 // here writing return is optional only when the result can be returned in one line
    
// Union and intersection types
    
    // union = this or that
    type FrontEndDeveloper = "Javascript developer" | "React Developer " 
    type FullStackDeveloper = "FrontEnd developer" | "BackEnd developer" 

    type ExpertDeveloper = FrontEndDeveloper | FullStackDeveloper

    let juniorDeveloper: ExpertDeveloper = "Javascript developer"
    let juniorWebDeveloper: ExpertDeveloper = "BackEnd developer"
    

    type UserInformation = {
        name: string;
        email: string;
        gender :"male" | "female"
    }

    let userData: UserInformation = {
        name: "sayem",
        email: "sayem@gmail.com",
        gender : "male"
    }


//  inter section = this and that 
    
    type A = {
        skills: string[];
        role: string;

    }
    type B = {
        skills: string[];
        role: string;
    }

    type C = A & B 

    let d : C = {
        skills: ["front-End", "BackEnd"],
        role: "Junior Software Developer",
        
    }

// ternary operator 
    let userAge: number = 18 
    
    let checkIfAdult = userAge >= 18 ? "Adult" : "not adult"

    console.log(checkIfAdult)
// nullish and optional 
    
    const isAuthanticated = ""; 
    let result1 = isAuthanticated ?? "guest"; // this depends on null or undefined
    let result2 = isAuthanticated ? isAuthanticated : "guest"
    console.log({result1},{ result2 })

// optional chaining user?.name?.firstName ?? 'No firstname found' --> let user ={ name : {lastName: "Taher" }}


// never, unknown, nullable

// nullable
// never 

    const throwError = (msg: string) : never => {
        throw new Error(msg)
        
    }
    // throwError('Something went wrong! Try again later');


// type assertion 
    
    const checkValue = (value: string | number): string | number | undefined => {
        
        if (typeof value === "string") {
            const convertedValue = parseFloat(value) * 1000;
            return ` converted value to kg is  : ${convertedValue}`;
        }
        if (typeof value === "number") {
            return value * 1000
        }
        return undefined
    
    }
    
    const resultFromCheckValue1 = checkValue(1000) as number // use it when you explicitly know if the return type will be a number
    const resultFromCheckValue2 = checkValue("1000") as string 

    console.log(resultFromCheckValue2)

    type CustomErrorMessage = {
        message: string;
    }

    try {
        
    }
    catch (error) {
        console.log((error as CustomErrorMessage ).message);
    }


    // type alias vs type interface 

    // -->  type alias can be used for both primitive and non-primitive values
    // --> interface can be only be used for object type


    type User1 = {
        name: string;
        age: string;
        role: number

    }
    type User2 = {
        address : string

    }

    type UserWithRoles = User1 & User2 & { //using intersection ' & '  we are extending the data
        year : string
    } 
    
    let studentData: UserWithRoles = {
        name: "sayem",
        age: "24",
        role: 4669045,
        address: "Eindhoven",
        year : "2024"
    } 

    // now we are doing the same with interface 

    interface StudentsData { // --> for interface declaring we are not usein the equal sign.
        name: string;
        age: string;
            
    }
    interface UserWithRoles2 extends StudentsData { // using ' extends ' keyword we are extending the data 
        role : string
    }
    //  --> we can also extend type with interface. doesn't have to be interface and interface rather interface vs interface/type

    const studentsRegisteredData: UserWithRoles2 = {
        name: "Sayem",
        age: "24",
        role:"Student"
    }

    //  let's see how it works for an array 

    type StudentsRole = number[]

    interface StudentRole2 {
        [index : number ] : number // here the index of the arrays are numbers and the data type is  also number
    }

    const studentsArrayOfRoles: StudentRole2 = [5, 78, 98] 

    //  interfce and type for functions 

    type AddNumbers1 = (num1: number, number2: number) => number 
    
    interface AddNumbers2 {
        (num1:number, num2:number) : number
    }

    const addValuesOfNumbers: AddNumbers2 = (num1, num2) => {
        return num1 + num2
    }


    // ---> overall interface can be a good option while working with objects 

// -------------------------//
// ****************
// Generics in typescript or generic type 
    
    type Generics<T> = Array<T>  // here ' T ' means the type of values you're assigning or the type of the parameters

    const arrayOfNumbers : Generics<number> = [2, 4, 5, 6]
    const arrayOfStrings : Generics<string> = ["sayem", "gijs"]
    const arrayOfBooleans : Generics<boolean> = [false,true,true]

// generics for objects 
    
    let registredUserData: Generics<{ name: string;  age:number}> = [ // writing just Generics<object> is not recommended
        {
            name: "Sayem",
            age:24
        },
        {
            name: "rafeq",
            age: 27

        }
    ]

// generics for tuples --> tuples are an array but they are ' ordered data' and can contain values of 'different data type'. 
   
    type GenericsTuple<X, Y> = [X, Y]
    
    const singleUserData: GenericsTuple<string, { name: string, phoneNumber: number }> = ["Sayem Ibne Taher", { name: "Sayem", phoneNumber: +31456890 }]
    
    const userStringData : GenericsTuple<string,number> = ["Sayem", 24]
    
    
// Generics with interface 
    
    interface DevelopersHouse<T,X = null> {
        name: string;
        skills: {
            frontEnd: string,
            experience: number,
            degree: string
        };
        education: string;
        university: string;
        isGraduated: boolean;
        graduationYear?: number;
        background: T;
        highSchoolBg?: X;
    }

    type DevelopersBackground1 = {
        companyRegistrationYear: number;
        location: string;
        city : string
        
    }
    interface DevelopersBackground2{
        companyName: string;
        workedYear: number;

    }
    const detailsOfregisteredDeveloper1: DevelopersHouse<DevelopersBackground2> = {
        name: "sayem",
        skills: {
            frontEnd: "React",
            experience: 2,
            degree : "ICT"
        },
        education: "Bachelor",
        university: "Fontys University Of applied sciences",
        isGraduated: false,
        background: {
            companyName: "Bosch",
            workedYear: 2024
        }
        
    }
    interface DevelopersHighSchoolBg {
        location: string,
        city: string,
        graduationYear : number
    }
    const detailsOfregisteredDeveloper2: DevelopersHouse<DevelopersBackground1, DevelopersHighSchoolBg> =
      {
        name: "sayem",
        skills: {
          frontEnd: "React",
          experience: 2,
          degree: "ICT",
        },
        education: "Bachelor",
        university: "Fontys University Of applied sciences",
        isGraduated: false,
        background: {
            companyRegistrationYear: 2024,
        location: "Eindhoven",
        city : "Eindhoven"

        },
        highSchoolBg: {
            location: "Mirpur 14",
            city: "Dhaka",
            graduationYear : 2019
        }
      };

    
//  Function with generics 
    
    // normal function returning an array

    const returnArray = (value: string): string[] => {
        return [value]
    }

    //  generic function returning an array 

    const functionUsingGeneric = <T>(value: T): T[] => {
        return [value]
    }
    type ReturnUserData = {
      name: string;
      age: number;
    }
    interface ReturnUserData2 {
      name: string;
      age: number;
    }

    let returnedResultOfTheArray = functionUsingGeneric<ReturnUserData2>({ name: "sadat", age: 23 })
    let returnedResultOfTheArray2 = functionUsingGeneric<string>("Sayem")

//  create generic function with Tuple 
    
    const sumOfNumbers = <T, X>(value1: T, value2 :X ): [T, X] => {
        return [value1,value2]
    }
    
    // example 

    const addStudentToTheCourse = <T extends { name: string; id: number; email:string}>(value: T) => {
        const course = "Next Level Web Development"

        return { ...value,course}
    }

    interface DetOfAddedStudent {
        name: string;
        id: number;
        email: string;
        age: number;
    }

    const detOfStu: DetOfAddedStudent = {
        name: "Usama",
        email: "sayem@gmail.com",
        id:48675,
        age: 20,
    };

    const detailsOfAddedStudent = addStudentToTheCourse(detOfStu)
    console.log(detailsOfAddedStudent)

    // constraints typescript 
    // generic constraints with keyof operator

    const getKeysOfAnObject = <X, Y extends keyof X>(obj: X, key: Y) => {
        return obj[key]
    }
    const findResult = getKeysOfAnObject(detOfStu, "age")
    console.log(findResult)
    
    //  asynchronus typescript 

    // promise
    const createPromise = () : Promise<string> => {
        return new Promise<string>((res, rej) => {
            const data: string = "Data received"
            if (data) {
                res(data)
            }
            else {
                rej("Failed to fetch data")
            }
        })
    }

    const fetchData = async () : Promise<string> => {
        const getData : string = await createPromise()
        // console.log(getData);
        return getData

    }
    fetchData()

    // fetching data from the api 

    type APiData = [{ 
        userId: number;
        id: number;
        title: string;
        body: string;
    }]
    

    const fetchDataFromAPI = async () : Promise<APiData> => {
      
            const response = await fetch(
              "https://jsonplaceholder.typicode.com/posts"
            );
            const data  = await response.json();
            // console.log(data);
            return data;
        
       

    }
    fetchDataFromAPI()

    
// conditional type 
    
    type Car = {
        model: string;
        brand: string;
        year: number;
        autoPilot?: boolean;
    }
    type CheckCarValue<T> = T extends keyof Car ? true : false
    
    type ResultFoundForCarValueCheck = CheckCarValue<"autoPilot">


    // mapped type --> dynamically chnaging the data type of another type 

    type ValuesInNumber = {
        year: number;
        grade: number;
    }
    type MappedTypeValues = {
        [key in keyof ValuesInNumber] : string
    }

    // mapped with generics -- > best practice 
    type MappedTypeValues2<T> = {
        [key in keyof T] : T[key]
    }
    const mappedValuesFound: MappedTypeValues2<ValuesInNumber > =  {
        year: 2000,
        grade :4.5
    }

    // utility type 

    type CustomerDetails = {
        name: string;
        products: string[];
        age: number;
        securityId?: number;
        contactDetails: number;
    }
    type CustomerRegistry = Pick<CustomerDetails, "age" | "name">

    // Omiting keys from a certain type 

    type CustomerDetailsWithdraw = Omit<CustomerDetails, "products" | "contactDetails">

    // Required 
    type RequiredCustomerDetails = Required<CustomerDetails>

    // Partial  -- make the keys optional
    type PartialCustomerDetails = Partial<CustomerDetails> // type Partial<T> = { [ key in keyof T] ?  T[key] : undefined } 
    
    //  read only

    type PersonReadOnly = Readonly<CustomerDetails>
    
    // Record 

    type CustomerDetails3 = Record<string, string | number | string[]>
    
    const customerInfo1: CustomerDetails3 = {
        name: "a",
        location: "Eindhoven",
        contactDetails : 45666
        
    }
    const emptyObject: Record<string, unknown> = {}
   
    emptyObject.name = "Sayem"
     console.log(emptyObject);
    
    
}
```

---

## Overview

This combined documentation brings together the functionality, type guards, and object handling within the provided TypeScript files.
