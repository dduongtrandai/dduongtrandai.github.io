---
title: "Mối Quan Hệ Giữa Các Lớp Trong Lập Trình Hướng Đối Tượng"
---

# Mối Quan Hệ Giữa Các Lớp Trong Lập Trình Hướng Đối Tượng (OOP)

Trong lập trình hướng đối tượng (Object-Oriented Programming - OOP), việc hiểu rõ mối quan hệ giữa các lớp (classes) là cốt lõi để thiết kế hệ thống linh hoạt, dễ bảo trì và dễ mở rộng. Bài viết này sẽ trình bày chi tiết các loại quan hệ giữa các lớp, minh họa bằng ví dụ C++.

## 1. Association (Liên Kết)

Association là mối quan hệ đơn giản nhất giữa hai lớp: một lớp sử dụng lớp kia.

### Ví dụ:

```cpp
class Student {
public:
    void study() {
        std::cout << "Studying..." << std::endl;
    }
};

class Teacher {
public:
    void teach(Student& student) {
        student.study();
    }
};
```

## 2. Aggregation (Tổng Hợp)

Aggregation là mối quan hệ "có - và" (has-a), nhưng đối tượng con có thể tồn tại độc lập.

### Ví dụ:

```cpp
class Engine {
public:
    void start() {
        std::cout << "Engine started" << std::endl;
    }
};

class Car {
private:
    Engine* engine;
public:
    Car(Engine* eng) : engine(eng) {}
    void startCar() {
        engine->start();
    }
};
```

## 3. Composition (Thành Phần)

Composition cũng là "has-a" nhưng đối tượng con KHÔNG tồn tại độc lập, nó phụ thuộc hoàn toàn vào vòng đời của lớp cha.

### Ví dụ:

```cpp
class Heart {
public:
    void beat() {
        std::cout << "Heart beating..." << std::endl;
    }
};

class Human {
private:
    Heart heart;
public:
    void live() {
        heart.beat();
    }
};
```

## 4. Inheritance (Kế Thừa)

Inheritance cho phép một lớp con thừa hưởng tính năng từ lớp cha.

### Ví dụ:

```cpp
class Animal {
public:
    void eat() {
        std::cout << "Eating..." << std::endl;
    }
};

class Dog : public Animal {
public:
    void bark() {
        std::cout << "Barking..." << std::endl;
    }
};
```

## 5. Dependency (Phụ Thuộc)

Lớp này sử dụng lớp khác tạm thời, thường là qua thàm số trong hàm.

### Ví dụ:

```cpp
class Logger {
public:
    void log(const std::string& message) {
        std::cout << "Log: " << message << std::endl;
    }
};

class Application {
public:
    void run(Logger& logger) {
        logger.log("Application started");
    }
};
```

## Kết Luận

Việc nắm vững mối quan hệ giữa các lớp giúc lập trình viên thiết kế hệ thống rõ ràng, dễ hiểu và linh hoạt. Từ đó, tăng cường khả năng tái sử dụng và bảo trì mã nguồn.
