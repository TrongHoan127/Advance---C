# Advance---C
<details><summary>LESSON 1: COMPILER - MARCO</summary>
    <p>
        
## LESSON 1: COMPILER - MARCO
### Compiler
- Trong ngôn ngữ lập trình, Compiler (trình phiên dịch) là chương trình có nhiệm vụ xử lý chương trình ngôn ngữ bậc cao thành ngôn ngữ bậc thấp hơn để máy tính thực thi.
- Quá trình biên dịch gồm các giai đoạn như sau:
![maxresdefault](https://github.com/user-attachments/assets/3fbcf4bf-b3b6-41e9-8d26-e33c72ee3287)
#### Preprocessor (Tiền xử lý)
- Bộ tiền xử lý có nhiệm vụ thực hiện: 
    - Nhận mã nguồn, source code (gồm: c, .h, .cpp, .hpp,...)
    - Xóa bỏ tất cả các chú thích, comments của chương trình
    - Chỉ thị tiền xử lý ( bằng dấu #) cũng được xử lý
    - Đầu ra là file i
       ```c
       gcc -E main.c -o main.i
 #### Compiler 
 - Chuyển từ ngôn ngữ bậc cao sang ngôn ngữ bậc thấp assembly. Đầu vào là file .i, đầu ra file .s.
    ```c
    gcc main.i -S -o main.s
#### Assembler 
- Chuyển sang mã máy (0,1). Đầu vào là file .s, đầu ra là file .o hay còn gọi là file object.
  ```c
    gcc - c main.s -o main.o
#### Linker
- Liên kết các file object.o lại thành một chương trình duy nhất.
  ```c
     gcc test1.o test2.o main.o -o main
### Macro
- Chỉ thị tiền xử lý là những chỉ thị cung cấp cho bộ tiền xử lý các thông tin trước khi quá trình phiên dịch bắt đầu. Các chỉ thị tiền xử lý bắt đầu bằng ký tự #
   - #include (file header): Chèn nội dung của file vào vị trí mình chỉ định vào file i. Giúp chương trình dễ quản lí
     ```c
     #include <stdio.h>
     #include "test1.h"
   - #define: Được sử dụng để định nghĩa các hằng số hoặc các đoạn mã thay thế, không có kiểu dữ liệu. Việc sử dụng #define để định nghĩa được gọi là Macro, nơi nào có tên Macro sẽ được thay thế bằng nội dung của Macro đó
  - Ví dụ 1:
	 ```c
    	 #include <stdio.h>
		#define PI 3.14 // Định nghĩa hằng số Pi sử dụng #define//
		int main() {
		double radius = 5.0; // Sử dụng hằng số Pi trong chương trình //
		double area = PI * radius * radius;
	
		printf("Radius: %.2f\n", radius);
		printf("Area of the circle: %.2f\n", area);
	
		return 0;
		}
  - Ví dụ 2:
   	  ```c
   	  #include <stdio.h>

		// Định nghĩa macro để tìm số lớn hơn giữa hai số
		#define MAX(x, y) ((x) > (y) ? (x) : (y))
		
		int main() {
		int a = 10, b = 20;
		
		// Sử dụng macro để tìm số lớn hơn giữa a và b
		int maxNumber = MAX(a, b);
		
		printf("The bigger number between %d and %d is: %d\n", a, b, maxNumber);
		
		return 0;
		}
  - #undef: Để hủy định nghĩa một #define đã được định nghĩa trước đó.
    ```c
    #include <stdio.h>
	#define MAX_SIZE 100
	
	int main() {
	    printf("MAX_SIZE is defined as: %d\n", MAX_SIZE);
	    
	    // Bỏ định nghĩa của MAX_SIZE
	    #undef MAX_SIZE
	    
	    // Định nghĩa lại MAX_SIZE với giá trị khác
	    #define MAX_SIZE 50
	    
	    printf("MAX_SIZE is now redefined as: %d\n", MAX_SIZE);
	
	return 0;
	}
  - #if, #elif, #else: Kiểm tra điều kiện của Marco.
  	- #if: Sử dụng để bắt đầu 1 điều kiện xử lý.Nếu đúng thì các dòng lệnh sau #if sẽ được biên dịch , sai sẽ bỏ qua đến khi gặp #endif.
	- #elif: Để thêm 1 ĐK mới khi #if hoặc #elif sai.
	- #else: Dùng khi không có ĐK nào đúng
	- #ifdef: Dùng để kiểm tra 1 macro định nghĩa hay chưa.Nếu định nghĩa rồi thì mã sau ifdef sẽ được biên dịch.
	- #ifndef: Dùng để kiểm tra 1 macro định nghĩa hay chưa.Nếu chưa định nghĩa thì mã sau #ifndef sẽ được biên dịch.Thường dùng để kiểm tra macro đó đã dc định nghĩa trong file nào chưa, kết thúc thì #endif
   - Ví dụ 1:
	    ```c
	    #include <stdio.h>
		// Định nghĩa một macro
		#define VERSION 3
		
		int main() {
		    // Sử dụng #if, #elif, #else
		    #if VERSION == 1                               // Điều kiện #if sai, nếu không còn kiểm tra điều kiện nào
		                                                    // nữa đi tới #endif luôn
		    printf("This is version 1.\n");
		    #elif VERSION == 2                             // Tiếp tục kiểm tra với #elif
		    printf("This is version 2.\n");            
		    #else                                          // Không có điều kiện nào ở trên đúng
		    printf("This is another version.\n");
		    #endif
		
		return 0;
		}
	- Ví dụ 2:
  	 ```c
		    #include <stdio.h>
		// Định nghĩa một macro
		#define FEATURE_ENABLED
		
		int main() {
		    // Kiểm tra xem FEATURE_ENABLED đã được định nghĩa đúng không?
		    #ifdef FEATURE_ENABLED
		    printf("Feature is enabled.\n");
		    #endif
		    
		    // Kiểm tra xem ANOTHER_FEATURE chưa được định nghĩa đúng không?
		    #ifndef ANOTHER_FEATURE
		    printf("Another feature is not enabled.\n");
		    #endif
		
		return 0;
		}
#### Macro funtion 
- Macro function là khi đoạn mã sử dụng #define với tham số truyền vào để hoạt động giống như một hàm.

- Nếu macro function có nhiều dòng, mỗi dòng (trừ dòng cuối) phải kết thúc bằng ký tự \.
  ```c
	#include <stdio.h>
	
	#define DISPLAY_SUM(a,b)                        \
	printf("This is macro to sum 2 number\n");      \
	printf("Result is: %d", a+b);
	
	int main() {
		DISPLAY_SUM(5,6);
	return 0;
	}
- Ưu điểm của macro function so với function là tối ưu về tốc độ, nhưng không tối ưu về bộ nhớ.
#### Toán tử trong Macro
- Toán tử # (stringizing operator) chuyển đối số của macro thành chuỗi.
- Toán tử ## (concatenation operator) nối các đối số lại với nhau thành một chuỗi hoặc tên mới.
- Các toán tử này giúp tạo ra các macro linh hoạt và mạnh mẽ hơn, cho phép bạn thao tác với chuỗi và tên biến trong quá trình biên dịch.
- ví dụ 1:
  ```c
	   #include <stdio.h>
	
	#define TO_STRING(x) #x
	
	int main() {
	    int a = 5;
	    printf("Giá trị của a là: %s\n", TO_STRING(a));  // Kết quả sẽ là "a"
	    return 0;
	}
- ví dụ 2:
  ```c
	  #include <stdio.h>
	
	#define CONCAT(x, y) x ## y
	
	int main() {
	    int xy = 10;
	    printf("Giá trị của xy là: %d\n", CONCAT(x, y));  // Kết quả sẽ là 10
	    return 0;
	}
  - Trong ví dụ trên, CONCAT(x, y) sẽ nối x và y lại với nhau thành xy. Kết quả là việc gọi CONCAT(x, y) sẽ được thay thế bằng xy, do đó giá trị của biến xy là 10.
#### Variadic Marco
- Variadic macro là một loại macro trong ngôn ngữ C (và C++) cho phép bạn định nghĩa macro nhận một số lượng đối số không xác định (hay còn gọi là đối số biến đổi). Điều này hữu ích khi bạn muốn tạo một macro có thể làm việc với nhiều đối số mà không cần phải xác định số lượng đối số cụ thể.
- Giả sử bạn muốn định nghĩa một macro LOG có thể nhận một số lượng tham số không xác định để in ra một thông báo cùng với các tham số đó:
	```c
	#include <stdio.h>
	
	#define LOG(fmt, ...) printf(fmt, __VA_ARGS__)
	
	int main() {
	    int a = 10;
	    float b = 3.14;
	    
	    LOG("a = %d, b = %.2f\n", a, b);  // Gọi macro với 2 tham số
	    LOG("Only one parameter: %d\n", a);  // Gọi macro với 1 tham số
	
	    return 0;
	}
- Giải thích:

- LOG(fmt, ...) là variadic macro. fmt là tham số bắt buộc, còn ... đại diện cho các tham số còn lại (tùy chọn).
- Trong thân macro, bạn sử dụng __VA_ARGS__ để đại diện cho các tham số bổ sung được truyền vào macro.
- __VA_ARGS__ là một biến đặc biệt trong ngôn ngữ C giúp lấy tất cả các tham số được truyền vào macro.
- Kết quả của chương trình trên sẽ là:
	- a = 10, b = 3.14
	- Only one parameter: 10
</details>

<details><summary>LESSON 2: STDARG- ASSERT</summary>
    <p>	
	    
 ## LESSON 2: STDARG - ASSERT	
 ### Thư viện STDARG
 - Thư viện <stdarg.h> trong C cung cấp các cơ chế để làm việc với các tham số biến (variadic parameters) trong các hàm và macro. Đây là một thư viện rất hữu ích khi bạn muốn định nghĩa các hàm hoặc macro có thể nhận một số lượng tham số không cố định, chẳng hạn như các hàm printf hoặc scanf.
 - Thư viện này cung cấp ba macro chính giúp bạn làm việc với các tham số biến:
	- va_list: Đây là kiểu dữ liệu được sử dụng để giữ thông tin về các tham số biến. Bản chất là con trỏ kiểu char được định nghĩa lại tên bằng typedef: typedef char* va_list;
	- va_start: Dùng để khởi tạo một đối tượng va_list và bắt đầu xử lý các tham số biến. Hàm này mang các kí tự vào chuỗi, tạo một con trỏ có giá trị bằng địa chỉ kí tự đầu tiên của chuỗi không xác định và thực hiện vòng lặp so sánh các kí tự trong chuỗi có giống với từng kí tự của label count không và con trỏ địa chỉ tăng dần dần ứng với địa chỉ của các kí tự tiếp theo của chuỗi. Sau khi xác định được kí tự giống với label count thì mới bắt đầu mang các kí tự sau dấu , vào chuỗi. 
	- va_arg: Dùng để lấy giá trị của một tham số biến trong danh sách tham số và ép kiểu dữ liệu thành kiểu dữ liệu mong muốn
	- va_end: Dùng để kết thúc việc truy cập các tham số biến và giải phóng tài nguyên.
- Cú pháp của các macro trong <stdarg.h>:
	- va_list:Được sử dụng để khai báo một biến sẽ chứa các tham số biến.
		```c

		va_list args;
	- va_start: Dùng để bắt đầu truy xuất các tham số biến. va_start nhận hai đối số: Đối số đầu tiên là biến va_list bạn đã khai báo. Đối số thứ hai là tên của tham số cuối cùng trong danh sách tham số cố định (tham số trước danh sách tham số biến).
		```c

		va_start(args, last_fixed_param);
	- va_arg:Dùng để truy xuất một tham số trong danh sách tham số biến. Bạn cần chỉ định kiểu dữ liệu của tham số bạn muốn truy xuất.
		```c

		type arg = va_arg(args, type); //type là kiểu dữ liệu của tham số bạn muốn lấy (ví dụ: int, double, char, ...).
	- a_end: Dùng để kết thúc truy xuất các tham số biến và giải phóng tài nguyên. Đây là bước quan trọng để tránh rò rỉ tài nguyên.
		```c

		va_end(args);
- Ví dụ về việc sử dụng <stdarg.h>:
- Ví dụ: Viết một hàm sum nhận một số lượng tham số không xác định và tính tổng các tham số đó.
	```c

	#include <stdio.h>
	#include <stdarg.h>
	
	// Hàm sum với các tham số biến
	int sum(int num, ...) {
	    int total = 0;
	    
	    // Khai báo va_list để truy cập các tham số biến
	    va_list args;
	    
	    // Khởi tạo va_list, đối số thứ hai là tham số cuối cùng cố định (num)
	    va_start(args, num);
	    
	    // Duyệt qua các tham số và tính tổng
	    for (int i = 0; i < num; i++) {
	        total += va_arg(args, int);  // Lấy giá trị của tham số kiểu int
	    }
	    
	    // Kết thúc truy xuất tham số biến
	    va_end(args);
	    
	    return total;
	}
	
	int main() {
	    int result = sum(4, 1, 2, 3, 4);  // Gọi sum với 4 tham số
	    printf("Tổng là: %d\n", result);  // Kết quả sẽ là 10
	    
	    return 0;
	}
- Giải thích:

	- Hàm sum nhận một tham số đầu vào num xác định số lượng tham số tiếp theo.
	- Sau đó, hàm sử dụng va_start để khởi tạo danh sách tham số biến và va_arg để lấy từng giá trị từ danh sách tham số.
	- Cuối cùng, va_end được gọi để kết thúc quá trình truy xuất tham số biến.

### Thư viện ASSERT	
- Thư viện assert.h là thư viện để hỗ trợ debug chương trình.

- Hàm assert(): dùng để kiểm tra điều kiện, nếu đúng thì chương trình tiếp tục còn sai thì dừng lại ngay lập tức và báo lỗi.

- Ví dụ báo lỗi chia cho 0:
  ```c
	#include <stdio.h>
	#include <assert.h>
	
	double thuong(int a, int b) {
	    assert( b != 0 && "Mẫu bằng 0");
	    return (double) a/b;
	}
	
	int main() {
	    printf("Thuong: %f\n", thuong(6, 0)); 
	    return 0;
	}
- Báo lỗi:
	```c
	> Assertion failed: b != 0 && "Mẫu bằng 0", file tempCodeRunnerFile.c, line 5
- Thường thấy hơn sẽ sử dụng macro để định nghĩa một lỗi.
	```c
	#include <stdio.h>
	#include <assert.h>
	#define LOG(condition, cmd) assert(condition && #cmd)
	
	double thuong(int a, int b) {
	    LOG(b != 0, "Mau bang bang 0");
	}
	
	int main() {
	    thuong(6,0);
	    return 0;
	}

</details>


<details><summary>LESSON 3: POINTER</summary>
    <p>
        
## LESSON 3: POINTER
### Khái niệm và các loại Pointer
Trong ngôn ngữ lập trình C, con trỏ (pointer) là một biến chứa địa chỉ bộ nhớ của một đối tượng (biến,hàm,mảng) khác. Việc sử dụng con trỏ giúp chúng ta thực hiện các thao tác trên bộ nhớ một cách linh hoạt hơn. Dưới đây là một số khái niệm cơ bản về con trỏ trong C:
#### Cách khai báo: 
   
    int *ptr;  // con trỏ đến kiểu int
    char *ptr_char;  // con trỏ đến kiểu char
    float *ptr_float;  // con trỏ đến kiểu float
- Lấy địa chỉ của một biến:
   ```c 
    int x = 10;
    int *ptr_x = &x;  // ptr_x giờ đây chứa địa chỉ của x
- Sử dụng con trỏ để truy cập giá trị:
    int y = *ptr_x;  // y sẽ bằng giá trị của x
 ![image](https://github.com/user-attachments/assets/2799e903-2562-470a-b884-70fd4158ad98)
     - chú ý: địa chỉ con trỏ đang trỏ tới: ptr = 0x01; địa chỉ của con trỏ: &ptr = 0xf1;giá trị tại địa chỉ con trỏ trỏ tới *ptr = *(0x01)=5
- Kích thước của con trỏ sẽ phụ thuộc kiến trúc máy tính và trình biên dịch. Ta có thể dùng sizeof() để kiểm tra kích thước của con trỏ:
  ```c 
  #include <stdio.h>
  int main() {
    int *ptr;
    printf("Size of pointer: %lu bytes\n", sizeof(ptr));
    return 0;
  }


- Ví dụ:
  ```c
  #include <stdio.h>
  void swap(int *a, int *b)
  {
    int tmp = *a;
    *a = *b;
    *b = tmp;

  }
  int main()
  {
   int a = 10, b = 20;
   swap(&a, &b);

   printf("value a is: %d\n", a);
   printf("value b is: %d\n", b);

    return 0;
  }

 #### Các loại Pointer:
##### Void pointer:
- Void pointer thường dùng để trỏ để tới bất kỳ địa chỉ nào mà không cần biết tới kiểu dữ liệu của giá trị tại địa chỉ đó.
  ```c
  void *ptr_void;
- Ví dụ:
  ```c
     #include <stdio.h>
     #include <stdlib.h>

     int main() {
   
	    int value = 5;
	    double test = 15.7;
	    char letter = 'A';
	   
	    void *ptr = &value;
	    printf("value is: %d\n", *(int*)(ptr));
	
	    ptr = &test;
	    printf("value is: %f\n", *(double*)(ptr));
	
	    ptr = &letter;
	    printf("value is: %c\n", *(char*)(ptr));
	   
	    return 0;
       }


#### Pointer to Constant:
- Định nghĩa một con trỏ không thể thay đổi giá trị tại địa chỉ mà nó trỏ đến thông qua dereference nhưng giá trị tại địa chỉ đó có thể thay đổi.
- Ví dụ:
  ```c
	#include <stdio.h>
	#include <stdlib.h>
	
	int main() {
	    
	    int value = 5;
	    int const *ptr_const = &value;
	
	    //*ptr_const = 7; // wrong
	    //ptr_const++; // right
	    
	    printf("value: %d\n", *ptr_const);
	
	    value = 9;
	    printf("value: %d\n", *ptr_const);
	
	    return 0;
	}


#### Constant Pointer:
- Định nghĩa một con trỏ mà giá trị nó trỏ đến (địa chỉ ) không thể thay đổi. Tức là khi con trỏ này được khởi tạo thì nó sẽ không thể trỏ tới địa chỉ khác.
- Ví dụ:
  ```c
	#include <stdio.h>
	#include <stdlib.h>
	
	
	int main() {
	    
	    int value = 5;
	    int test = 15;
	    int *const const_ptr = &value;
	
	    printf("value: %d\n", *const_ptr);
	
	    *const_ptr = 7;
	    printf("value: %d\n", *const_ptr);
	
	    //const_ptr = &test; // wrong
	    
	    return 0;
	}




#### Function pointer:
- Pointer to function (con trỏ hàm) là một biến mà giữ địa chỉ của một hàm. Có nghĩa là, nó trỏ đến vùng nhớ trong bộ nhớ chứa mã máy của hàm được định nghĩa trong chương trình.
- Trong ngôn ngữ lập trình C, con trỏ hàm cho phép bạn truyền một hàm như là một đối số cho một hàm khác, lưu trữ địa chỉ của hàm trong một cấu trúc dữ liệu, hoặc thậm chí truyền hàm như một giá trị trả về từ một hàm khác.
- Ví dụ:
  ```c
	#include <stdio.h>
	
	// Hàm mẫu 1
	void greetEnglish() {
	    printf("Hello!\n");
	}
	
	// Hàm mẫu 2
	void greetFrench() {
	    printf("Bonjour!\n");
	}
	
	int main() {
	    // Khai báo con trỏ hàm
	    void (*ptrToGreet)();
	
	    // Gán địa chỉ của hàm greetEnglish cho con trỏ hàm
	    ptrToGreet = greetEnglish;
	
	    // Gọi hàm thông qua con trỏ hàm
	    (*ptrToGreet)();  // In ra: Hello!
	
	    // Gán địa chỉ của hàm greetFrench cho con trỏ hàm
	    ptrToGreet = greetFrench;
	
	    // Gọi hàm thông qua con trỏ hàm
	    (*ptrToGreet)();  // In ra: Bonjour!
	
	    return 0;
	}

- Trong ví dụ này, ptrToGreet là một con trỏ hàm có thể trỏ đến các hàm greetEnglish và greetFrench. Việc này giúp linh hoạt trong việc chọn và sử dụng hàm tương ứng tại thời điểm chạy.
- Ví dụ 2:
  ```c
	#include <stdio.h>
	
	void sum(int a, int b)
	{
	    printf("Sum of %d and %d is: %d\n",a,b, a+b);
	}
	
	void subtract(int a, int b)
	{
	    printf("Subtract of %d by %d is: %d \n",a,b, a-b);
	    
	}
	
	void multiple(int a, int b)
	{
	    printf("Multiple of %d and %d is: %d \n",a,b, a*b );
	    
	}
	
	void divide(int a, int b)
	{
	    if (b == 0)
	    {
	        printf("Mau so phai khac 0\n");
	        return;
	    }
	    
	    printf("%d divided by %d is: %f \n",a,b, (double)a / (double)b);
	    
	}
	
	void calculator(void (*ptr)(int a, int b), int a, int b)
	{
	    printf("Program calculate: \n");
	    ptr(a,b);
	}
	
	int main()
	{
	    void (*ptrToFunc)(int,int);
	    ptrToFunc = &divide;
	
	    calculator(ptrToFunc,5,2);
	
	    return 0;
	}



	
- Trong ví dụ này, ptrToFunc là một con trỏ hàm trỏ đến các hàm sum, subtract, multiple, divide. Hàm calculator với 3 tham số truyền vào là: con trỏ hàm, a, b, và sẽ call function mà con trỏ đang trỏ tới và truyền vào 2 tham số a và b.
Pointer to pointer:
#### Con trỏ đến con trỏ (Pointer to Pointer)
- là một kiểu dữ liệu trong ngôn ngữ lập trình cho phép bạn lưu trữ địa chỉ của một con trỏ. Con trỏ đến con trỏ cung cấp một cấp bậc trỏ mới, cho phép bạn thay đổi giá trị của con trỏ gốc. Cấp bậc này có thể hữu ích trong nhiều tình huống, đặc biệt là khi bạn làm việc với các hàm cần thay đổi giá trị của con trỏ.
 - Ví dụ:
   ```c

	#include <stdio.h>
	
	int main() {
	    int value = 42;
	    int *ptr1 = &value;  // Con trỏ thường trỏ đến một biến
	
	    int **ptr2 = &ptr1;  // Con trỏ đến con trỏ
	
	    printf("Value: %d\n", **ptr2);
	
	    return 0;
	      }
- Trong ví dụ này:
	- ptr1 là một con trỏ thường trỏ đến biến value.
	- ptr2 là một con trỏ đến con trỏ, trỏ đến địa chỉ của ptr1.
	- Khi sử dụng **ptr2, chúng ta có thể truy cập giá trị của biến value.
#### NULL pointer
 - Null Pointer là một con trỏ không trỏ đến bất kỳ đối tượng hoặc vùng nhớ cụ thể nào. Trong ngôn ngữ lập trình C, một con trỏ có thể được gán giá trị NULL để biểu diễn trạng thái null.
 - Ví dụ:
    ```c
	#include <stdio.h>
	
	int main() {
	    int *ptr = NULL;  // Gán giá trị NULL cho con trỏ
	
	    if (ptr == NULL) {
	        printf("Pointer is NULL\n");
	    } else {
	        printf("Pointer is not NULL\n");
	    }
	
	    return 0;
	}

- Trong ví dụ này:
	- Con trỏ ptr được khai báo và được gán giá trị NULL.
	- Một điều kiện kiểm tra xem con trỏ có trỏ đến một đối tượng nào đó hay không.
	- Nếu con trỏ bằng NULL, chương trình in ra "Pointer is NULL", ngược lại nếu con trỏ không bằng NULL, chương trình in ra "Pointer is not NULL".
	- Sử dụng null pointer thường hữu ích để kiểm tra xem một con trỏ đã được khởi tạo và có trỏ đến một vùng nhớ hợp lệ chưa. Tránh dereferencing (sử dụng giá trị mà con trỏ trỏ đến) một null pointer là quan trọng để tránh lỗi chương trình.
</details>
   
 <details><summary>LESSON 6: GOTO - SETJMP</summary>
  <p>
  
 ## LESSON 6: GOTO - SETJMP
 ### GOTO
- goto là một từ khóa trong ngôn ngữ lập trình C, cho phép chương trình nhảy đến một câu lệch đã được đặt trước đó trong cùng một hàm. Mặc dù nó cung cấp khả năng kiểm soát flow của chương trình, nhưng việc sử dụng goto thường được xem là không tốt vì nó có thể làm cho mã nguồn trở nên khó đọc và khó bảo trì.
- Cách sử dụng goto trong C/C++:
	-Cú pháp:

	```c

	goto label;
- Trong đó: label là một nhãn (label) được định nghĩa trước trong chương trình, là tên của vị trí mà bạn muốn nhảy đến. Nhãn này phải kết thúc bằng dấu hai chấm (:).
- Ví dụ:

	```c

	#include <stdio.h>
	
	int main() {
	    int x = 10;
	
	    if (x == 10) {
	        goto jump_here; // Nhảy đến nhãn jump_here nếu x == 10
	    }
	
	    printf("Không bao giờ đến đây.\n"); // Dòng này sẽ bị bỏ qua vì goto đã nhảy qua
	
	jump_here:
	    printf("Đã nhảy đến nhãn jump_here.\n");
	
	    return 0;
	}
 
- Giải thích ví dụ:
	- Câu lệnh goto jump_here;: Chương trình sẽ nhảy đến vị trí có nhãn jump_here: ngay khi điều kiện if (x == 10) đúng.
	- jump_here:: Đoạn mã sau nhãn này sẽ được thực thi khi chương trình nhảy tới đó.
	- Dòng "Không bao giờ đến đây." sẽ không bao giờ được in ra vì câu lệnh goto đã chuyển điều khiển ra ngoài đoạn mã đó
  ### SETJMP
  - setjmp.h là một thư viện trong ngôn ngữ lập trình C, cung cấp hai hàm chính là setjmp và longjmp. Cả hai hàm này thường được sử dụng để thực hiện xử lý ngoại lệ trong C, mặc dù nó không phải là một cách tiêu biểu để xử lý ngoại lệ trong ngôn ngữ này.
- Cú pháp:
  	```c

	#include <setjmp.h>
	
	int setjmp(jmp_buf env);
- Trong đó:
	- jmp_buf env: Là một mảng hoặc cấu trúc được sử dụng để lưu trữ thông tin trạng thái của ngữ cảnh chương trình tại thời điểm gọi setjmp. Nó sẽ chứa thông tin cần thiết để chương trình có thể quay lại điểm gọi hàm setjmp.
	- Hàm setjmp trả về giá trị 0 khi nó được gọi lần đầu tiên, và sẽ trả về giá trị khác (thường là một giá trị không bằng 0) khi chương trình quay lại từ hàm longjmp.
- Mô tả:
	- setjmp được sử dụng để lưu lại trạng thái của ngữ cảnh chương trình tại một điểm cụ thể (gọi là "checkpoint").
	- longjmp sau đó có thể được sử dụng để quay lại điểm đó, thay vì tiếp tục chạy từ vị trí mà chương trình bị tạm dừng.
- Cách hoạt động:
	- Gọi setjmp: Khi setjmp được gọi, nó lưu lại trạng thái của chương trình (ví dụ, các thanh ghi, con trỏ, v.v.) trong biến env (được khai báo kiểu jmp_buf).
	- Quay lại với longjmp: Khi gặp lỗi hoặc cần nhảy ra một điểm khác trong chương trình, bạn có thể gọi hàm longjmp(env, value) để quay lại điểm gọi setjmp, đồng thời trả về giá trị value từ hàm setjmp. Điều này làm cho chương trình "nhảy" về lại điểm đó.
- Ví dụ về cách sử dụng setjmp và longjmp:
	```c

	#include <stdio.h>
	#include <setjmp.h>
	
	jmp_buf env;

	void func() {
	    printf("Bắt đầu func.\n");
	    longjmp(env, 1);  // Quay lại setjmp và trả về giá trị 1
	    printf("Không bao giờ in dòng này.\n");
	}
	
	int main() {
	    if (setjmp(env) == 0) {
	        // Đây là lần gọi đầu tiên của setjmp
	        printf("Điều khiển đang ở trong main.\n");
	        func();  // Gọi hàm func, sau đó longjmp sẽ quay lại đây
	    } else {
	        // Sau khi longjmp được gọi
	        printf("Điều khiển quay lại từ longjmp.\n");
	    }
	
	    return 0;
	}
- Giải thích ví dụ:
	- Gọi setjmp(env) lần đầu tiên: Khi setjmp được gọi trong hàm main, chương trình lưu trạng thái ngữ cảnh vào biến env và trả về giá trị 0. Sau đó, chương trình tiếp tục bình thường và gọi hàm func().
	- Gọi longjmp(env, 1) trong func: Trong hàm func, câu lệnh longjmp(env, 1) sẽ khiến chương trình quay lại điểm gọi setjmp trong hàm main. Lúc này, setjmp không trả về 0 nữa mà trả về giá trị 1, vì vậy đoạn mã trong else sẽ được thực thi.
- Kết quả chương trình:
	```css
	Điều khiển đang ở trong main.
	Bắt đầu func.
	Điều khiển quay lại từ longjmp.
