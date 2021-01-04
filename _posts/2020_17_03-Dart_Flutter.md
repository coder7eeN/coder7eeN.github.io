# Dart và Flutter, tại sao không?

###### *Writter: Huy Phạm - March, 2019* 

Khi nhắc đến việc làm sao để tạo ra 1 ứng dụng mobile thì thứ mọi người sẽ lặp tức nghĩ ngay đến là **native app (Android và iOS)**, nhưng bên cạnh đó vẫn còn rất nhiều công nghệ có thể giúp bạn tạo ra 1 ứng dụng mobile như **Cordova, Webview (WeChat), Ionic, Xamarin và React Native**. Tất cả các framework, platform đó đều hổ trợ người dùng tạo ra được 1 ứng dụng mobile theo ý muốn của mình. Và để không bỏ lỡ cuộc vui thì Google cũng đã mang đến cho người dùng đứa con mới nhất của mình - **Flutter** - nó kế thừa cũng như nổi bật hơn các công nghệ hybrid app kia. Vậy thì làm sao để có thể sử dụng, có thể tạo ra được những sản phẩm theo ý muốn của mình? Bài viết với những kiến thức của bản thân mình sẽ đem đến cho bạn có được 1 số kiến thức cơ bản nhất để có thể tự mình "chiến" và "khám phá" Flutter.

## Dart Language
<!--**(tìm đọc, dart worst langugae lấy thông tin, phân biệt library.. huy trần, )**-->

Bao giờ cũng vậy, bạn muốn "chiến" hoặc "chỉ học để biết" 1 library, 1 framework, 1 platform thì **ngôn ngữ (language)** sử dụng để build lên nó là cái bạn cần phải quan tâm và tìm hiểu, cũng giống như 1 chiếc xe nếu không có xăng thì cũng chỉ để ngắm. 

Flutter sử dụng ngôn ngữ Dart để lập trình, ngôn ngữ Dart ra đời từ năm 2011, nhắm đến tạo ra ứng dụng chạy đa nền tảng - web, mobile, desktop và IoT nhưng lúc ấy cộng đồng còn khá nhỏ và cũng không phải là sự lựa chọn cho các công ty (vì đây là ngôn ngữ phát triển bởi chính Google và các công ty cũng rất e dè điều này). Khi Google phát triển 1 os mới (operation system) - **Fuchsia** - thì Flutter được chọn làm nền tảng cho các ứng dụng đến lúc này thì Dart mới có được nhiều người biết đến và cộng đồng được mở rộng hơn.

Phiên bản hiện tại lúc viết bài này là 2.2. Những bản 1.x và 2.0 vẫn còn khá nhiều lỗi khiến coder lúc viết khá lúng túng, trình biên soạn vẫn còn chưa support tốt, tuy nhiên với việc ra bản 2.1 thì mọi thứ đã tốt hơn rất nhiều. 

Dart là ngôn ngữ đơn giản, dễ tiếp cận và cũng khá dễ hiểu. Dart là ngôn ngữ tĩnh, theo hướng đối tượng (object oriented programming), functional programming và lexical scoped. Nó như 1 sự kết hợp giữa Java và JavaScript nên khi học nó nếu ai đã có nền tảng 1 trong 2 ngôn ngữ kia thì lúc tiếp cận sẽ khá dễ. Dart hỗ trợ khai báo biến linh hoạt (loose and strong typing) với cú pháp (syntax) kiểu C và biên dịch kiểu JavaScript. Okay, vài dòng giới thiệu về ngôn ngữ, giờ sẽ không mất thêm thời gian hãy đi vào coi thử làm sao để "code" với Dart.

<!--tìm hiểu cách JS biên dịch-->

#### 1. Project structure
<!--tham khảo phần tools trong trang chủ-->
<!--đọc thêm về YAML-->

- Thư mục bin: đây là nơi chứa các file public tools để chạy Dart scripts.
- Thư mục lib: đây là nơi chứa các file public libraries để import vào trong các file ở thư mục bin.
- pubspec.yaml: nơi import dependency, quản lí phiên bản của Dart, etc.. nó tương tự gradle trong Android và được viết bằng YAML language.

#### 2. Important concepts

Đây là phần chú ý đầu tiên khi bạn đọc trên trang chủ của Dart. Vì thế hãy đọc kỹ hướng dẫn trước khi liều.

1. Bất kì thứ gì có thể đặt vào 1 biến đều là `object` và mọi object đều là thể hiện của 1 `class`. Số, hàm, `null` đều là object. Mọi object thì đều xuất phát từ Object class.
2. Tuy Dart là strong typed nhưng Dart vẫn hỗ trợ loose typed. Có nghĩa là nếu bạn chưa chắc chắn về kiểu dữ liệu cho biến thì vẫn có thể khai báo với kiểu dynamic.
3. Dart hỗ trợ generic type, ví dụ `List<int>` và `List<dynamic>`.
4. Dart hỗ trợ top-level function (như hàm main()). Bạn có thể tạo ra 1 hàm bên trong hàm khác (nested hoặc local function).
5. Dart cũng hỗ trợ top-level variables. 
6. Không như Java, Dart không có các từ khóa để set access modifier. Nếu 1 indentifier bắt đầu với ( _ ) thì nó là *private* trong library của nó.
7. Identifier có thể bắt đầu bằng một chữ cái hoặc dấu gạch dưới ( _ ).
8. Dart vừa hỗ trợ *expressions*, vừa hỗ trợ *statements*. Bạn có thể sử dụng biểu thức `? exp1 : exp2` và cũng có thể sử dụng câu lệnh`if else`.
9. Dart tools có thể báo cho bạn 2 loại vấn đề: warnings và errors. Warnings là những dấu hiểu chỉ ra rằng code của bạn có thể không hoạt động, nhưng chương trình của bạn vẫn có thể chạy. Errors có thể là error lúc compile-time hoặc run-time. Error lúc compile-time hiển nhiên sẽ khiến code bạn không chạy được, còn kết quả của error run-time sẽ là những exceptions được throw ra khi chạy.

#### 3. Variables

- String - để thao tác với chuỗi và kí tự.

	```dart
	String name = 'huy pham';
	```
	
- num - để thao tác với số.

	```dart
	num number = 17;
	num number1 = 17.03;
	```

	- int - để thao tác với số nguyên.
	- double - để thao tác với số thập phân.
- bool - để khai báo biến boolean.

	```dart
	bool isCheck = true;
	```
	
- const - để khai báo biến hằng.

	```dart
	const int id = 123;
	```

- dynamic - có thể dùng để khai báo cả chuỗi và số. 

	```dart
	dynamic name = 'huy pham';
	dynamic age = 25;
	dynamic isHandsome = true;
	```

- var - để khai báo biến khi chưa biết là chuỗi hay số, không thể dùng để khai báo kiểu trả về của hàm.

	```dart
	var text = 'hello guys';
	```

- Runes - để sử dụng các emoji.

	```dart
	Runes clap = Runes('\u{1f44f}');
	print(String.fromCharCodes(clap));
	```
		
Tất cả biến trong Dart đều không phải là dạng nguyên thủy nó đều là đối tượng.
	
#### 4. Collection

- Enumerated types - còn được gọi là enum, một kiểu class đặc biệt sử dụng để biểu diễn một tập hợp giá trị không đổi.

	```dart
	enum color {
		red,
		blue,
		green,
		orange
	}
	```
	
- List - một collection thông dụng, dùng để tập hợp các phần tử vào 1 mảng, trong Dart chi có object list và nó làm hết công việc của ArrayList như add, remove, insert.

	```dart
	List<num> numbers = [0, 1, 2, 3, 4, 5];
	List mixin = [69, 'kimochi', true]; // List<dynamic>
	```

- Map - 1 object thông dụng khác, chứa cặp key-value. Dart hỗ trợ map literals và kiểu dữ liệu Map.

	```dart
	Map roles = {'H': 'dev', 'U': 'tester', 'Y': 'designer'};
	
	Map<String, int> languages = Map();
	languages.putIfAbsent('java', () => 1890);
	languages.putIfAbsent('dart', () => 2011);
	languages.putIfAbsent('java', () => 1995);
	```
 
- Set - tập hợp các giá trị không theo thứ tự và không lặp lại giá trị đã có.

	```dart
	Set<int> numbers = new Set<int>();
	numbers.add(3);
	numbers.add(2);
	numbers.add(2);
	numbers.add(7);
	
	var age = {1, 'a', true};
	```

- Queue - 1 collection có thể thao tác cả 2 đầu vào của mình. 1 đầu để đưa dữ liệu và 1 đầu xóa dữ liệu. Hữu dụng khi xây dựng collection theo kiểu first in, fist out.

	```dart
	Queue numbers = new Queue();
	```

#### 5. Flow control

- assert - ngắt 1 thực thi thông thường khi điều kiện trả về sai.

	```dart
	assert(name == 'huy');
	```

- if else - như mọi ngôn ngữ khác, sử dụng để điều hướng.

	```dart
	if(condition) {
		// do something
	} else {
		// do another
	}
	```

- switch case - như mọi ngôn ngữ khác, cũng sử dụng để điều hướng.

	```dart
	var condition;
	switch(condition) {
		case decision:
			// do something;
			break;
		case decison1: 
			// do another thing;
			break;
		default:
			// do default result;
			break;
	```

- Loop - vòng lặp.
	- while 

	```dart
	while(condition) {
		// do something
	}
 	```
	
	- do while 

	```dart
	do {
		// do something
	} while(condition);
	```
	
	- for loop

	```dart
	List alphabets = ['alpha', 'beta', 'gamma', 'delta', 'epsilon', 'zeta'];
	
	// for with index
	for(int i = 0; i < alphabets.length; i++) {
		// do something
	}
	
	// for each item
	for(var word in alphabets) {
		// do something
	}
	
	alphabets.forEach((String item) {
		// do something
	});
	```
	
#### 6. Function

- Basic function - Dart là ngôn ngữ hướng đối tượng, hàm trong Dart cũng là một object và có một kiểu dữ liệu cho nó. Điều đó có nghĩa là có thể gán 1 function cho 1 biến hoặc dùng nó làm đối số (argument) cho 1 hàm khác.

	```dart
	bool isYourName(String name) {
		return name == 'huy pham';
	}
	```
	
	- Nếu không khai báo kiểu dự liệu thì sẽ mặc định là void hoặc tùy vào kết quả trả về của hàm.

	```dart
	isYourName(String name) {
		return name == 'huy pham';
	}
	```
	
	- Để rút gọn thì ta nên dùng cú pháp `=>` đối với hàm không có block code.

	```dart
	isYourName(String name) => name == 'huy pham';
 	```

- Optional named parameter function - khi gọi hàm bạn có thể chỉ định tên tham số đã khai báo trong hàm và gọi tham số tùy ý không cần quan tâm đến thứ tự của nó.

	```dart
	void declareYourCharacter(bool isHumorous, {bool isQuiet, bool isKind = false}) {
		// do something
	}
	
	declareYourCharacter(true, isKind: true, isQuiet: true);
	
	```

- Optional unnamed parameter function - bạn có thể tạo ra 1 tham số tùy chọn khi khởi tạo hàm, lúc gọi làm bạn có thể truyền hoặc không truyền đối số vào cho nó và phải gọi đúng thứ tự như lúc khởi tạo.

	```dart
	void declareYourCharacter(bool isHumorous, [bool isQuiet, bool isKind = false]) {
		// do something
	}
	
	declareYourCharacter(true, true, true);
	```

- Anonymous function - hầu hết mọi hàm đều có 1 cái tên để thể hiện hàm đó làm gì nhưng chúng ta vẫn có thể khởi tạo 1 hàm không tên và gọi nó là anonymous function hoặc có thể là lambda hoặc là closure. Anonymous function được khởi tạo lúc chạy runtime, nó có thể gán cho 1 biến, gọi 1 hàm khác.

	```dart
	var alphabets = ['alpha', 'beta', 'gamma', 'delta', 'epsilon', 'zeta'];
	
	alphabets.forEach((String item) {
		print('${alphabets.indexOf(i)item);
	});
	
	var sayHello = () => print('Hello guys');
	
	sayHello();
	```

#### 7. Some basic JavaScript's knowledge 

- Lexical scope
- Closure
- Anonymous function
- Callback
- Promise
- Async await

#### 7. Null aware operation

- `?:` (Ternary Operator) - đa số ngôn ngữ đều hỗ trợ, thay thế cho if else.

	```dart
	height < 175 ? 'Short' : 'Tall';
	```
	
- `??` - toán tử kiểm tra null, nếu biến trả về bằng null thì nó sẽ gán biến đó cho 1 giá trị mặc định.

	```dart
	String name = user.name() ?? 'huy pham';
	```
	
- `??=` - kiểm tra biến có null không, nếu biến null thì gán giá trị nếu không thì không thực thi.

	```dart
	Alphabet alphabet;
	alphabet ??= Alphabet('alpha');
	```

- `?.` - truy cập vào 1 method hoặc 1 object, nếu nó không null, ngược lại thì trả về null.

	```dart
	Alphabet alphabet;
	// nếu aphabet có giá trị character thì gán cho biến character ngược lại quăng ra exception
	String character = alphabet?.character;
	
	// tốt hơn thì nên gán giá trị mặc định nếu giá trị trả về là null
	String character = alphabet?.character ?? 'alpha';
	```

#### 8. Classes

<!--Class và constructor vẫn còn nhiều cái để nói nhưng chỉ nêu ra cái cơ bản nhất-->
Dart là ngôn ngữ hướng đối tượng với các class và thừa kế dựa trên mixin (mixin-based inheritance). Mỗi object đều là thể hiện của 1 class và tất cả class đều xuất phát từ Object class. *Thừa kế dựa trên mixin* có nghĩa là mỗi class đều có 1 superclass (trừ Object class), phần bên trong của mỗi class đều có thể được tái sử dụng trong nhiều class được phân cấp.

- Create a class

	```dart
	class Vehicle {
		int wheel;
		int speed;
	}
	```

- Constructor

	```dart
	class Vehicle {
		int wheel;
		int speed;
	}
	
	Vehicle(this.wheel; this.speed);
	```

#### 9. Object oriented programming

- Encapsulation - tính bao đóng là đối tượng được bảo vệ không cho các truy cập từ code bên ngoài như thay đổi trạnng thái hay nhìn trực tiếp. Tính bao đóng của Dart được thể hiện bằng cách khai báo ( _ )trước biến hoặc hàm, phạm vi hoạt động của nó là trong library chứa nó và kể cả khi import thì bạn cũng không thể gọi trực tiếp được.

	```dart
	int _x;
	
	void _init() {
		// do something
	} 
	```

- Inheritance - tính kế thừa là khả năng cho ta xây dựng class dựa trên tính chất của class đã có. Đó là class Cha, các class Con phát sinh từ class Cha và đương nhiên nó cũng sẽ được thừa kế tính chất của Cha. Class Con có thể sử dụng các tính chất như định nghĩa ở class Cha thông qua super hoặc có thể định nghĩa lại.

	```dart
	class Vehicle {
		void countNumberOfWheels(int wheel) {
			print('This vehicle has $wheel wheels');
		}
	}
	
	class Bike extends Vehicle {
		@override
		void countNumberOfWheels(int wheel) {
			super.countNumberOfWheels(wheels);
		}
	}
	```

- Polymorphism - tính đa hình là các object trong cùng 1 họ tuân thủ theo 1 thể hiện nhưng có thể thực thi theo nhiều cách khác nhau.
	- Override - khi cùng 1 phương thức nhưng cách bên trong phương thức đó thực hiện ở từng nơi lại khác nhau. Ví dụ phương thức `countNumberOfWheels` ở ví dụ trên, xe máy sẽ trả về 2 nhưng xe ô tô lại trả về 4.
	- Overload - không được support trong Dart nhưng bạn có thể sử dụng optional parameter để thay thế, cùng 1 phương thức nhưng có tham số khai báo trong nó có thể được xài hay không được xài.
- Abstraction - tính trừu tượng là sự tập trung vào các tính chất cối lõi nhất của 1 object, loại bỏ đi những tính chất rườm rà xung quanh.

	```dart
	abstract class Vehicle {
		void honk();
		void speed();
	}
	
	// extend toàn bộ phương thức được khai báo trong Vehicle 
	// có thể thừa kế lại những tính chất đã định nghĩa trong class Vehicle thông qua super
	class Motobike extends Vehicle {
		@override
		void honk() {
			super.honk();
		}
		
		@override
		void speed() {
			print('Very fast');
		}
	}
	```

- Interface - Dart không hổ trợ từ khóa interface để khai báo nhưng mỗi class đều định nghĩa là một interface.

	```dart
	class Vehicle {
		//phải định nghĩa phương thức đó để làm gì
		void honk() => print('honk honk);
		void speed() => print('322 km/h');
	}
	
	// implement toàn bộ phương thức được khai báo trong Vehicle 
	// nó sẽ không thừa kế lại từ Vehicle và bạn phải định nghĩa lại phương thức đó sẽ làm gì
	class Motobike implements Vehicle {
		@override
		void honk() {
			print('beep beep');
		}
		
		@override
		void speed() {
			print('Very fast');
		}
	}
	```

- Mixins và mixin - đây là khái niệm khiến nhiều người khi tiếp xúc với Dart khá lúng túng. Vậy mixin là gì? Mixins là gì? và liệu một chiếc xe máy có thể chạy trên nước?
	- Mixins - cách để trừu tượng hóa và tái sử dụng code trong các class khác nhau.

	```dart
	class Motobike {
		bool isRunFast() {
			return true;
		}
		
		void show() {
			print('This is a motobike');
		}
	}
	
	class Plane {
		bool isFlyHigh() {
			return true;
		}
		
		void show() {
			print('This is a plane');
		}
	}
	
	class Ship() {
		bool isRunInWater() {
			return true;
		}
		
		void show() {
			print('This is a ship');
		}
	}
	
	mixin Mixin on Ship {
		@override
		bool isRunInWater() {
			super.isRunInWater();
		}
		
		bool isHaveSail() {
			return true;
		}
	}
	
	class Scooter extends Motobike with Plane, Ship {...}
	
	main() {
		Scooter myScooter = Scooter();
		myScooter.isRunFast(); // true
		myScooter.isFlyHigh(); // true
		myScooter.isFlyHigh(); // true
		myScooter.show(); // This is a ship
	}
	```
	
	- Như ví dụ trên, class Scooter có thể sử dụng các thương thức được khai báo ở các class Motobike, Plane, Ship mà không gặp phải một trở ngại gì. Đây chỉ là cách để tái sử dụng lại code trong Dart chứ không phải là đa thừa kế, đừng nhầm lẫn chỗ này. 
	- Tương tự, khi gọi phương thức `show()` thì kết quả trả về là `This is a ship`, bởi vì khi extend qua các class như vậy thì các class đó sẽ được sếp vào 1 stack theo tuyến tính. Class Motobike được extend đầu tiên sẽ nằm trên đầu, sau đó lần lượt các class Plane và Ship sẽ xếp sau trong stack. Vì là last in, first out nên khi thực thi thì phương thức `show()` ở class Ship sẽ được thực thi.
	- mixin - khai báo việc có thể áp dụng mixin vào class. Class Mixin có thể extends hoặc implements các phương thức được khai báo ở class Ship(). Khi khởi tạo với từ khóa mixin thì trong class đó chỉ có khai báo các phương thức, bạn không thể khởi tạo constructor hoặc getter, setter. Đây giống như 1 chiếc thùng chứa tất cả các phương thức, khi nào bạn cần sử dụng phương thức nào thì extends hoặc implements đến nó và lấy ra sử dụng.
	
**All right, hy vọng với những kiến thức cơ bản này thì mình mong bạn đã có thể tự tin tự mình tiếp tục "khám phá" Dart. Và những kiến thức nâng cao hơn như asynchronous, generic, socket hoặc BLoC pattern thì mình sẽ nói đến ở những bài viết theo, hy vọng các bạn tiếp tục ủng hộ :)**

## Flutter framework

Flutter là 1 mobile SDK do Google phát triển, nó giúp người dùng có thể tạo ra được 1 ứng dụng chạy trên cả iOS và Android. Là một Cross-flatform framework nhưng khác với các Cross-flatform hiện tai, Flutter không thông qua bridge, mà nó sẽ chạy engine render riêng (viết bằng C++) và dùng Flutter framework (viết bằng Dart) để giao tiếp với các service. Cả 2 bộ này sẽ được đóng gói cùng ứng dụng và thông qua SDK nó có thể chạy trên đa nền tảng. Kì vọng mà team phát triển Flutter nhắm đến là có thể chạy trên đa nền tảng, Flutter ngoài chạy trên mobile thì còn có thể chạy trên nền web thông qua dự án mang tên Hummingbird, chạy trên các thiết bị IoT và cả desktop. Tuy vậy, Flutter cũng còn rất "non trẻ", nó cần thêm thời gian để có thể phát triển hơn nữa và việc chọn Flutter để học cũng là 1 cách để đầu tư cho tương lai.

![alt](https://cdn-images-1.medium.com/max/800/1*UpoHX3az39ZqkFwBr_gndA.png)

Sau gần 1 năm với các phiên bản preview thì phiên bản stable 1.0 của nó được ra mắt vào sự kiện Flutter Live (4/12/2018) và phiên bản hiện tại lúc mình viết bài này là 1.2.2.

Để bắt đầu tìm hiểu thì chúng ta sẽ đi vào tìm hiểu về lifecycle cụ thể là stateful widget lifecycle và stateless widget lifecycle, đối với mình tìm hiểu về lifecycle là điều đầu tiên mình quan tâm khi tìm hiểu về framework nào đó. Bởi vì hiểu được lifecycle thì chúng ta sẽ dễ dàng tiếp cận và biết được nó sẽ hoạt động như thế nào. Ở đây mình sẽ viết theo những gì mình biết và mình hiểu nên có sai sót hoặc thiếu xót cần góp ý thì hãy comment phía dưới cho mình :)

#### 1. Widget and Widget tree

- Trong Flutter, mọi thứ đều là **Widget**. Widget là thứ mà bạn có thể nhìn thấy, có thể tương tác với ứng dụng của bạn.
- Widget được tổ chức thành dạng cây, gồm có parent Widget và children Widgets. 

	```dart
	@override
	Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Demo'),
      ),
      body: Center(
        child: Column(
          children: <Widget>[
            Text('Hello guys'),
            Text('Welcome to my article'),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _onPressed,
        child: Icon(Icons.add),
      ),
     );
   }
	```
	
	- Như ví dụ trên, Scaffold là parent Widget chứa 3 children widgets là Center, Column và Text. Ta sẽ có được sơ đồ widget tree như sau:

	![alt](https://cdn-images-1.medium.com/max/800/1*z_A9htJmE6THrxZeloVRiw.png)
	###### *Ảnh của Didier Boelens*
	
#### 2. BuildContext

- BuildContext là tham chiếu đến vị trí của mỗi widget trên widget tree. Mỗi widget có 1 BuildContext thể hiện. Nếu 1 widget có các children widgets thì BuildContext của widget đó cũng sẽ là parent BuildContext của các children BuildContexts chứa trong nó. Điều đó có nghĩa chúng ta sẽ có một BuildContext tree.

	![alt](https://cdn-images-1.medium.com/max/800/1*Tc0kB9YXL4Bj6tonRJlH0w.png)
	###### *Ảnh của Didier Boelens*

#### 3. StatelessWidget

- Đây là những widget không quan tâm đến việc thay đổi, tạo ra 1 lần duy nhất hoặc hiểu cách đơn giản hơn thì đây là widget chỉ nhận khởi tạo có sẵn rồi thực thi nó và không có thay đổi State. Ví dụ như widget Text, Center, MaterialApp, ...
- Cấu trúc của một StatelessWidget như sau:

	```dart
	class MyWidget extends StatelessWidget {
	  MyWidget({Key key, this.param,}) : super(key: key);
	  String param;
	  
	  @override
	  Widget build(BuildContext context) {
	    return Container(
	      child: Text('Hello guys'),
	    );
	  }
	}
	```
	
	- Bạn có thể thấy, chúng ta có thể thêm vài tham số vào constructor. Tuy nhiên, hãy nhớ rằng những tham số này sẽ không thay đổi (immutable) ở những lần build sau.
	- Lifecycle của StatelessWidget gồm: 
		- Khởi tạo
		- Render widget thông qua build()

#### 4. StatefulWidget

- Trái ngược với StatelessWidget thì StatefulWidget sẽ xử lí các dữ liệu bên trong nó, lắng nghe những thay đổi, dữ liệu này sẽ liên tục thay đổi (mutable) trong suốt lifecycle của widget.
- Tập hợp những dữ liệu thay đổi được giữ bởi StatefulWidget, thay đổi trong suốt lifecycle của widget và dữ liệu có thể đọc 1 cách đồng bộ khi widget đã được build thì ta gọi đó là State. State định nghĩa ra phần hành vi mà StatefulWidget thể hiện. 1 State chứa các thông tin tương tác với widget thông qua các khía cạnh về hành vi (behavior) và layout. Mỗi khi thay đổi State thì widget đó sẽ thay đổi theo.
- Giữa State và BuildContext có 1 mối quan hệ khá khăn khít. Mỗi khi 1 State được tạo ra thì nó sẽ gắn với 1 BuildContext và lúc này State là *mounted*.

#### 5. StatefulWidget lifecycle

- Lifecycle của StatefulWidget được thể hiện như sau:
	- createState()
	- mounted == true
	- initState()
	- didChangeDependencies()
	- build()
	- didUpdateWidget()
	- setState()
	- deactivate()
	- dispose()
	- mounted == false  

	```dart
	class MyWidget extends StatefulWidget {
	  @override
	  _MyWidgetState createState() => _MyWidgetState();
	}

	class _MyWidgetState extends State<MyWidget> {
	
	  @override
	  void initState() {
	    super.initState();
	  }
	
	  @override
	  void didChangeDependencies() {
	    super.didChangeDependencies();
	  }
	
	  @override
	  Widget build(BuildContext context) {
	    return null;
	  }
	
	  @override
	  void didUpdateWidget(TestMain oldWidget) {
	    super.didUpdateWidget(oldWidget);
	  }
	
	  @override
	  void setState(fn) {
	    super.setState(fn);
	  }
	
	  @override
	  void deactivate() {
	    super.deactivate();
	  }
	
	  @override
	  void dispose() {
	    super.dispose();
	  }
	  
	}
	```
	
	- createState() - khi tạo ra 1 StatefulWidget thì createState() sẽ được gọi để tạo ra State cho widget và thêm widget vào widget tree.
	- mounted == true - khi chúng ta đã tạo ra State thì 1 BuildContext sẽ được gán cho State.
	- initState() - đây là phương thức đầu tiên được gọi lúc ta khởi tạo widget. Nó được gọi 1 và chỉ 1 lần duy nhất và khi override lại thì cần phải gọi lại super.initState(). Chúng ta sử dụng phương thức này cho:
		- Khởi tạo dữ liệu cho 1 BuildContext cụ thể
		- Khởi tạo các thuộc tính cho parent widget
		- Khi chúng ta đăng kí 1 Stream, khởi tạo dữ liệu hoặc thay đổi dữ liệu của widget
	- didChangeDependencies() - đây là phương thức tiếp theo sẽ được gọi sau khi initState() được khởi tạo. Override phương thức này có nghĩa là widget đã được liên kết với 1 InheritedWidget hoặc bạn muốn State lắng nghe sự thay đổi của widget được thừa kế . Một khi đã liên kết widget với InheritedWidget thì mỗi khi widget rebuild thì phương thức này sẽ được gọi.
	- build() - đây là phương thức sẽ được gọi mỗi khi State thay đổi hoặc là khi InheritedWidget cần thông báo cho các widget đã đăng kí.
	- didUpdateWidget() - phương thức được gọi nếu parent widget thay đổi hoặc có widget cần rebuild, nhưng nó cần phải cùng runtimeType. Flutter có cơ chế tái sử dụng State trong thời gian dài, do đó, trong trường hợp này ta cần khởi tạo lại dữ liệu.
	- setState() - đây là phương thức mà bạn sẽ phải "vọc" khá nhiều khi làm việc với Flutter. Nó thông báo cho framework biết dữ liệu đã thay đổi và widget nên rebuild lại. setState() nhận 1 callback đồng bộ.
	- deactivate() - hiếm khi ta phải đụng đến phương thức này, bởi vì nó được gọi khi 1 widget bị xóa khỏi widget tree nhưng có thể thêm vào lại nếu frame vẽ lên widget đó chưa kết thúc. Phương thức này được tạo để phục vụ việc di chuyển State từ điểm này đến điểm khác trên widget tree.
	- dispose() - gọi khi State đã được xóa hoàn toàn.
	- mounted == false - khi này State không thể nào remount lại được nữa.

#### 6. StatefulWidget or StatelessWidget?

- Nếu widget của bạn sẽ phải thường xuyên thay đổi State và khi thay đổi thì widget của bạn sẽ được rebuild thì bạn nên sử dụng StatefulWidget. Còn nếu widget của bạn State từ lúc khởi tạo đến lúc kết thúc vẫn không có gì thay đổi thì bạn nên sử dụng StatelessWidget.
- Ví dụ widget của bạn là 1 TextField, bạn cần phải biết được State lúc nào nó được nhập, lúc nào nó đã được nhập xong, State của nó thay đổi liên tục. Còn nếu widget của bạn chỉ là 1 Text hiển thị thông báo và nó không bao giờ thay đổi thì bạn nên sử dụng StatelessWidget.

#### 7. Some common widgets

Ở bài viết này mình chỉ liệt kê và giới thiệu tên vào widget thường hay dùng nên sẽ không đi sâu vào các thuộc tính của nó. Sẽ có 1 bài viết hoặc nhiều bài viết khác mình giới thiệu về các widget trong Flutter. Thế giới widget trong Flutter rất đa dạng nên 1 bài viết chẳng thể nào nói hết được sự thú vị của nó. Đây là thứ hấp dẫn mình đến với Flutter, cảm giác khi làm việc với các widget y như khi bạn chơi với một bộ lego, bạn tha hồ lắp ghép và sáng tạo với nó.

- Text - hiển thị nội dung bạn muốn thông báo và bạn có thể custom nó thông qua thuộc tính style với khá nhiều thứ thú vị.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return Text('Hello guys');
	  }
	```

- TextField - giúp bạn có thể nhập nội dung từ bàn phím.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return TextField();
	  }
	```
	
- RaisedButton - nút bấm giúp bạn có thể truy cập đến các phần khác nhau tùy theo ý muốn của bạn. Widget này bắt buộc bạn phải truyền vào 1 callback cho thuộc tính onPressed.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return RaisedButton(onPressed: _onPressed,);
	  }
	```
	
- Scaffold - đây là 1 widget cung cấp cho bạn một giao diện hoàn chỉnh gồm phần appbar, body và 1 floatingActionButton chính hiệu Google. 

	```dart
	@override
	  Widget build(BuildContext context) {
	    return Scaffold();
	  }
	```
	
- Container - widget thông dụng cung cấp 1 widget con, nó là wiget vừa có các thuộc tính để padding và có các thuộc tính để margin, width và height. Nếu sử dụng widget này bạn sẽ tốn khá nhiều thời gian để bạn ngồi canh chỉnh  view sao cho đẹp nhất.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return Container(
	      child: Text('Hi guys'),
	    );
	  }
	```
	
- Center - widget giúp bạn canh giữa cho widget con bên trong, lúc đầu mình cũng khá "bối rối" với widget này vì việc canh giữa bây giờ đã được nâng lên một tầm cao mới nhưng đến khi xài nó thì cảm thấy khá tiện lợi.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return Center(
	      child: Text('Hi guys'),
	    );
	  }
	```
	
- Padding - widget đúng như tên của nó là padding widget con bên trong. Bạn bắt buộc phải khai báo thuộc tính padding của nó thông qua class EdgeInsetsGeometry.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return Padding(
	      padding: EdgeInsets.all(69.96),
	      child: Text('Hi guys'),
	    );
	  }
	```
	
- Expanded - widget giúp bạn bọc widget con bên nó và phân vùng hiển thị để không bị bể giao diện. Nó tương tự như *layout_weight* bên Android.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return Expanded(
	      child: Text('Hi guys'),
	    );
	  }
	```
	
- Row và Column - đây là 2 widget giúp bạn hiển thị tập hợp nhiều widget sắp xếp theo hàng hoặc cột. Nó tương tự như thuộc tính *orientation* trong *LinearLayout* của Android.

	```dart
	@override
	  Widget build(BuildContext context) {
	    return Row(
	      children: <Widget>[
	        Text('Hello guys'),
	        Text('This is row'),
	      ],
	    );
    }
	```
	
	```dart
	@override
	  Widget build(BuildContext context) {
	    return Column(
	      children: <Widget>[
	        Text('Hello guys'),
	        Text('This is column'),
	      ],
	    );
    }
	```
	
**Okay, mong rằng 1 vài hiểu biết cơ bản của mình về Flutter sẽ giúp bạn có hiểu được Flutter là gì và các khái niệm cơ bản khi bạn tiếp cận với Flutter.**

## Tham khảo

- [Widget — State — BuildContext — InheritedWidget](https://medium.com/flutter-community/widget-state-buildcontext-inheritedwidget-898d671b7956)
- [Dart: What are mixins?](https://medium.com/flutter-community/dart-what-are-mixins-3a72344011f3)

<!--conclusion-->

<!--Người ta ghét 1 ngôn ngữ hay 1 framework thì rất dễ 
nhưng để tìm ra cái hay cái độc thì phải suy xét rồi so sánh các kiểu-->

**Mỗi ngôn ngữ được tạo ra đều có chức năng riêng của nó, ngôn ngữ nào cũng có cái đẹp và sự độc đáo của nó. Hãy tìm hiểu với đam mê và sự hứng thú cao nhất, bạn sẽ khám phá được nhiều thứ hơn việc chỉ là "tìm hiểu về ngôn ngữ".**


<!--JS compile JS chỉ có 1 thread nên khi chạy 1 tiến trình thì tiến trình đó sẽ chạy vào thread, chạy vào stack, có 2 phần là main stack để chạy các tiến trình không có bất đồng bộ và stack queue để chạy các tiến trình bất đồng bộ, các tiến trình bất đồng bộ sẽ được gọi thông qua callback, nhưng sẽ bị rơi vào callback hell, promise hell, nên sẽ xài async await-->
	
	



	