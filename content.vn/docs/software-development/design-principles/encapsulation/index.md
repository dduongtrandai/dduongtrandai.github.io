---
title: "Tính Đóng Gói"
---

# Encapsulation trong Design Principles: Nguyên lý và Ứng dụng với C++

## Giới thiệu

Trong thế giới phát triển phần mềm, các nguyên lý thiết kế (Design Principles) đóng vai trò như la bàn định hướng cho các quyết định thiết kế của chúng ta. Một trong những nguyên lý cốt lõi nhất là **Encapsulation** - không chỉ là một khái niệm trong lập trình hướng đối tượng (OOP) mà còn là một nguyên tắc thiết kế phần mềm mạnh mẽ có thể nâng cao chất lượng code trong mọi hệ thống phần mềm.

Bài viết này sẽ khám phá Encapsulation từ góc độ nguyên lý thiết kế, tìm hiểu cách nó liên kết với các nguyên lý khác, và minh họa ứng dụng của nó thông qua các ví dụ C++ thực tế.

## Encapsulation không chỉ là tính đóng gói của OOP

Mặc dù Encapsulation thường được giới thiệu như một trong bốn trụ cột của OOP, nó thực sự vượt xa khái niệm kỹ thuật đơn thuần và trở thành một nguyên lý thiết kế phần mềm quan trọng.

### Định nghĩa rộng hơn:

Trong bối cảnh các nguyên lý thiết kế, Encapsulation là:

> Quá trình đóng gói dữ liệu và hành vi liên quan vào một đơn vị gắn kết, đồng thời giới hạn truy cập vào chi tiết triển khai nội bộ, chỉ hiển thị giao diện được xác định rõ ràng cho bên ngoài.

## Các khía cạnh cốt lõi của Encapsulation trong thiết kế phần mềm

### 1. Che giấu thông tin (Information Hiding)

Information hiding (được Robert C. Martin gọi là "Ẩn những gì thay đổi") là yếu tố cốt lõi của Encapsulation. Điều này có nghĩa là:

- Che giấu các chi tiết triển khai phức tạp
- Ẩn dữ liệu dễ biến đổi
- Giới hạn phạm vi tác động của thay đổi
- Bảo vệ tính toàn vẹn bên trong của module

```cpp
// Ví dụ về Information Hiding trong C++
class DatabaseConnection {
private:
    // Chi tiết triển khai được ẩn
    std::string connectionString;
    void* connectionHandle;
    bool isEncrypted;
    std::vector<void*> preparedStatements;
    
    // Phương thức nội bộ
    void authenticateConnection() {
        // Chi tiết xác thực phức tạp
    }

public:
    // Interface đơn giản, rõ ràng
    bool connect();
    bool disconnect();
    QueryResult executeQuery(const std::string& query);
    bool isConnected() const;
};
```

### 2. Đóng gói liên kết dữ liệu và hành vi (Bundling Related Data and Behavior)

Encapsulation thúc đẩy việc đóng gói các dữ liệu liên quan và hành vi của chúng vào một đơn vị gắn kết. Điều này thực hiện nguyên tắc "high cohesion" - một trong những nguyên tắc SOLID.

```cpp
// Bundling related data and behavior
class ShoppingCart {
private:
    std::vector<Product> items;
    double totalPrice;
    double taxRate;
    
    // Phương thức tính toán nội bộ
    void recalculateTotal() {
        totalPrice = 0;
        for (const auto& item : items) {
            totalPrice += item.getPrice() * item.getQuantity();
        }
        totalPrice += totalPrice * taxRate;
    }

public:
    void addItem(const Product& product);
    void removeItem(const std::string& productId);
    void updateItemQuantity(const std::string& productId, int quantity);
    double getTotalPrice() const;
    std::vector<Product> getItems() const;
};
```

### 3. Tạo ranh giới rõ ràng (Establishing Clear Boundaries)

Encapsulation xác định các ranh giới rõ ràng giữa các module, thành phần và lớp.

```cpp
// Module boundaries with namespaces
namespace Authentication {
    class UserManager {
        // Authentication functionality
    };
}

namespace Accounting {
    class InvoiceGenerator {
        // Accounting functionality
    };
}

// Trong code sử dụng
Authentication::UserManager userManager;
Accounting::InvoiceGenerator invoiceGenerator;
```

## Mối quan hệ với các Design Principles khác

Encapsulation không đứng một mình mà có mối quan hệ chặt chẽ với nhiều nguyên tắc thiết kế phần mềm khác:

### 1. Single Responsibility Principle (SRP)

SRP (một lớp chỉ nên có một lý do để thay đổi) được hỗ trợ trực tiếp bởi Encapsulation. Khi bạn đóng gói một tập hợp trách nhiệm liên quan, bạn tạo ra các lớp có trách nhiệm đơn lẻ.

```cpp
// Sai - Vi phạm SRP
class UserService {
public:
    User findUser(int id);
    void saveUser(User user);
    void sendEmail(User user, std::string message);
    bool validatePassword(std::string password);
    void generateReport(User user);
};

// Đúng - Tuân thủ SRP với Encapsulation
class UserRepository {
public:
    User findById(int id);
    void save(User user);
};

class EmailService {
public:
    void sendEmail(User user, std::string message);
};

class PasswordValidator {
public:
    bool validate(std::string password);
};

class ReportGenerator {
public:
    void generateUserReport(User user);
};
```

### 2. Law of Demeter (Principle of Least Knowledge)

Nguyên tắc này (một đối tượng chỉ nên giao tiếp với "bạn gần nhất") thúc đẩy Encapsulation. Nó hướng dẫn chúng ta ẩn các chi tiết bên trong và giảm sự phụ thuộc giữa các đối tượng.

```cpp
// Vi phạm Law of Demeter
void processCustomer(Customer customer) {
    Address address = customer.getAddress();
    ZipCode zipCode = address.getZipCode();
    City city = zipCode.getCity();
    city.processTax();
}

// Tuân thủ Law of Demeter với Encapsulation thích hợp
void processCustomer(Customer customer) {
    customer.processTax();  // Ẩn quá trình bên trong Customer
}
```

### 3. Interface Segregation Principle (ISP)

ISP (khách hàng không nên bị buộc phụ thuộc vào các phương thức mà họ không sử dụng) cũng liên quan mật thiết đến Encapsulation. Nó khuyến khích chúng ta chia các giao diện lớn thành các giao diện nhỏ hơn, tập trung hơn.

```cpp
// Vi phạm ISP
class MultiFunctionDevice {
public:
    virtual void print() = 0;
    virtual void scan() = 0;
    virtual void fax() = 0;
    virtual void copy() = 0;
};

// Triển khai cụ thể
class BasicPrinter : public MultiFunctionDevice {
public:
    void print() override { /* Code */ }
    void scan() override { throw NotSupportedException(); }  // Không hỗ trợ
    void fax() override { throw NotSupportedException(); }   // Không hỗ trợ
    void copy() override { throw NotSupportedException(); }  // Không hỗ trợ
};

// Tuân thủ ISP với Encapsulation thích hợp
class Printer {
public:
    virtual void print() = 0;
};

class Scanner {
public:
    virtual void scan() = 0;
};

class FaxMachine {
public:
    virtual void fax() = 0;
};

class Copier {
public:
    virtual void copy() = 0;
};

// Bây giờ có thể tạo ra các triển khai chỉ tập trung vào các chức năng cần thiết
class BasicPrinter : public Printer {
public:
    void print() override { /* Code */ }
};

class AdvancedMFD : public Printer, public Scanner, public FaxMachine, public Copier {
    // Triển khai tất cả các phương thức
};
```

## Kỹ thuật triển khai Encapsulation trong C++

### 1. Access Modifiers (public, private, protected)

C++ cung cấp các công cụ tích hợp để triển khai Encapsulation:

```cpp
class BankAccount {
private:  // Chỉ có thể truy cập bên trong class
    double balance;
    std::string accountNumber;
    std::vector<Transaction> transactions;

protected:  // Có thể truy cập bởi các lớp con
    void addTransaction(const Transaction& t);

public:  // Có thể truy cập từ bất kỳ đâu
    double getBalance() const;
    void deposit(double amount);
    bool withdraw(double amount);
};
```

### 2. Pimpl Idiom (Pointer to Implementation)

Đây là một kỹ thuật Encapsulation mạnh mẽ trong C++ cho phép ẩn hoàn toàn các chi tiết triển khai và giảm thiểu phụ thuộc:

```cpp
// Trong header file (public interface)
class Engine {
public:
    Engine();
    ~Engine();
    void start();
    void stop();
    int getRevolutions() const;

private:
    class EngineImpl;  // Chỉ khai báo tiến, không định nghĩa
    std::unique_ptr<EngineImpl> pImpl;  // Con trỏ đến triển khai
};

// Trong file cpp (private implementation)
class Engine::EngineImpl {
public:
    void start() { isRunning = true; }
    void stop() { isRunning = false; }
    int getRevolutions() const { return isRunning ? currentRPM : 0; }

private:
    bool isRunning = false;
    int currentRPM = 0;
    double fuelLevel = 100.0;
    std::vector<Cylinder> cylinders;
    CoolingSystem coolingSystem;
    // Nhiều chi tiết triển khai phức tạp khác...
};

// Triển khai Engine sử dụng EngineImpl
Engine::Engine() : pImpl(std::make_unique<EngineImpl>()) {}
Engine::~Engine() = default;
void Engine::start() { pImpl->start(); }
void Engine::stop() { pImpl->stop(); }
int Engine::getRevolutions() const { return pImpl->getRevolutions(); }
```

### 3. Namespaces và Internal Linkage

C++ cung cấp các cơ chế để Encapsulation ở mức module:

```cpp
// weather_module.h - Public interface
namespace Weather {
    struct WeatherData {
        double temperature;
        double humidity;
        double windSpeed;
    };

    WeatherData getCurrentWeather(const std::string& location);
    std::vector<WeatherData> getWeatherForecast(const std::string& location, int days);
}

// weather_module.cpp - Private implementation details
namespace {  // Anonymous namespace - chỉ hiển thị trong file này
    const std::string API_KEY = "secret_api_key";
    
    std::string buildApiUrl(const std::string& location) {
        return "https://weather.example.com/api?key=" + API_KEY + "&location=" + location;
    }
    
    Weather::WeatherData parseApiResponse(const std::string& jsonResponse) {
        // Implementation details
    }
}

namespace Weather {
    WeatherData getCurrentWeather(const std::string& location) {
        std::string url = buildApiUrl(location);
        std::string response = makeHttpRequest(url);
        return parseApiResponse(response);
    }
    
    // More implementation...
}
```

## Một ví dụ thực tế: Hệ thống thư viện

Hãy xem một ví dụ thực tế về thiết kế hệ thống quản lý thư viện sử dụng nguyên tắc Encapsulation:

```cpp
// LibrarySystem.h - Public interfaces
namespace Library {
    class Book {
    public:
        Book(const std::string& title, const std::string& author, const std::string& isbn);
        
        // Public interface - chỉ truy cập những gì cần thiết
        std::string getTitle() const;
        std::string getAuthor() const;
        std::string getISBN() const;
        bool isAvailable() const;
        
    private:
        // Implementation details hidden
        std::string title;
        std::string author;
        std::string isbn;
        bool available;
        
        // These methods are only accessible to "friend" classes
        void borrow();
        void returnBook();
        
        friend class LibraryManager;
    };
    
    class Member {
    public:
        Member(const std::string& name, const std::string& id);
        
        std::string getName() const;
        std::string getMemberId() const;
        std::vector<std::string> getBorrowedBooks() const;
        
    private:
        std::string name;
        std::string memberId;
        std::vector<std::string> borrowedBooks;
        
        void addBook(const std::string& isbn);
        void removeBook(const std::string& isbn);
        
        friend class LibraryManager;
    };
    
    class LibraryManager {
    public:
        bool addBook(const Book& book);
        bool removeBook(const std::string& isbn);
        bool registerMember(const Member& member);
        bool unregisterMember(const std::string& memberId);
        
        bool borrowBook(const std::string& memberId, const std::string& isbn);
        bool returnBook(const std::string& memberId, const std::string& isbn);
        
        std::vector<Book> searchBooks(const std::string& query) const;
        
    private:
        std::vector<Book> books;
        std::vector<Member> members;
        
        Book* findBook(const std::string& isbn);
        Member* findMember(const std::string& memberId);
    };
}
```

Trong ví dụ này:

1. **Information Hiding**: Chi tiết triển khai của `Book` và `Member` được ẩn đi. Người dùng không thể trực tiếp thay đổi trạng thái của sách hoặc danh sách sách đã mượn.

2. **Ranh giới rõ ràng**: `LibraryManager` đóng vai trò quản lý tương tác giữa các đối tượng. Nó định nghĩa ranh giới rõ ràng giữa hệ thống thư viện và phần còn lại của ứng dụng.

3. **Kiểm soát quyền truy cập**: Sử dụng `friend` class và `private` methods để chỉ cho phép `LibraryManager` thực hiện các hoạt động như mượn và trả sách.

4. **Interface rõ ràng**: Hệ thống cung cấp giao diện công cộng đơn giản và dễ hiểu cho phần còn lại của ứng dụng.

## Lợi ích của Encapsulation trong thiết kế phần mềm

Khi được áp dụng như một nguyên tắc thiết kế, Encapsulation mang lại nhiều lợi ích:

1. **Khả năng bảo trì cao hơn**: Thay đổi nội bộ không ảnh hưởng đến người dùng bên ngoài

2. **Giảm sự phức tạp**: Giao diện đơn giản, chi tiết triển khai được ẩn đi

3. **Bảo vệ tính toàn vẹn dữ liệu**: Kiểm soát truy cập và sửa đổi

4. **Giảm sự phụ thuộc**: Các module chỉ phụ thuộc vào giao diện, không phải chi tiết triển khai

5. **Khả năng mở rộng tốt hơn**: Dễ dàng thay đổi triển khai mà không ảnh hưởng đến code khác

6. **Khả năng tái sử dụng**: Các module được đóng gói tốt có thể dễ dàng được tái sử dụng

7. **Kiểm thử đơn giản hơn**: Giao diện rõ ràng giúp kiểm thử dễ dàng hơn

## Một số nguyên tắc và mẹo khi áp dụng Encapsulation

1. **Tell, Don't Ask**: Yêu cầu đối tượng thực hiện việc gì đó thay vì lấy trạng thái để tự thực hiện

2. **Dựa vào abstraction, không phải implementation**: Sử dụng giao diện và lớp trừu tượng để ẩn chi tiết triển khai

3. **Ẩn dữ liệu dễ thay đổi**: Những gì có khả năng thay đổi nên được đóng gói cẩn thận

4. **Chia nhỏ các giao diện**: Áp dụng Interface Segregation Principle

5. **Tách biệt interface và implementation**: Xem xét sử dụng các mẫu thiết kế như Bridge hoặc Adapter

## Kết luận

Encapsulation không chỉ đơn thuần là một khái niệm OOP; nó là một nguyên tắc thiết kế phần mềm mạnh mẽ có liên kết chặt chẽ với nhiều nguyên tắc thiết kế khác. Bằng cách đóng gói dữ liệu và hành vi, giới hạn quyền truy cập, và xác định ranh giới rõ ràng, chúng ta có thể xây dựng các hệ thống phần mềm dễ bảo trì, linh hoạt và mạnh mẽ hơn.

Khi thiết kế phần mềm, hãy nhớ suy nghĩ về Encapsulation không chỉ như một công cụ kỹ thuật, mà là một nguyên tắc thiết kế tổng thể hướng dẫn cách chúng ta cấu trúc hệ thống và tạo ra các ranh giới rõ ràng, mạnh mẽ giữa các thành phần.

---

## Tài liệu tham khảo

1. "Clean Code: A Handbook of Agile Software Craftsmanship" - Robert C. Martin
2. "Design Patterns: Elements of Reusable Object-Oriented Software" - Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides
3. "Effective C++: 55 Specific Ways to Improve Your Programs and Designs" - Scott Meyers
4. "The Pragmatic Programmer: Your Journey to Mastery" - Andrew Hunt, David Thomas