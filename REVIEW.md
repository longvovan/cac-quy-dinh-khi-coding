# Các quy định trước khi review Pull Request

- Đúng yêu cầu, mục đích của Task, Hot-fix, ...
- Áp dụng đúng Mô hình High-level Architecture MVC
- Convention cần phải đảm bảo: Dễ hiểu, dễ đọc, rõ ràng, tuân theo convention chung.

Ngoài ra khi coding phải làm theo quy chuẩn sau:
- [Một số quy chuẩn về viết code ruby.](#Một-số-quy-chuẩn-về-viết-code-ruby)
- [Các tiêu chuẩn về ngữ pháp.](#Các-tiêu-chuẩn-về-ngữ-pháp)
- [Cách đặt tên.](#Cách-đặt-tên)
- [Cách quy định trong Class.](#Cách-quy-định-trong-Class)


## Một số quy chuẩn về viết code ruby

- Lề (indent) là 2 khoảng trắng (white space)
- Không dùng tab
- Không để khoảng trắng ở cuối dòng trong một method
- Ở cuối dòng của file, phải để khoảng trắng.
- Trước và sau các toán tử, dấu hai chấm, sau dấu phẩy và dấu chấm phẩy, để 1 khoảng trắng.
- Trước dấu phẩy và dấu chấm phẩy không để khoảng trắng.

```
sum = 1
a, b = 1, 2
1 > 2 ? true : false
```

- Trong một dòng không viết quá 125 kí tự
- Nếu dài hơn 125 kí tự thì xuống dòng mới theo quy tắc sau.
  - Nếu xuống dòng khi đang ở giữa chuỗi method thì xuống dòng trước dấu . （dot) và đem dấu chấm xuống đầu dòng mới
```
"one string".something_long_long_method(arg1)
  .other_cool_long_method(arg2)
  .another_awsome_long_method(arg3)
```
- Cho phép 1 dòng có quá 125 ký tự trong trường hợp nguyên nhân là do chuỗi string literal dài.

```# ok
foo = "This is a very very long string that can't be broken down and may contain #{variable}"
```
- Trước và sau các dấu [] () không để khoảng trắng
- Riêng {} khuyến khích nên để khoảng trắng trước và sau.

```
a = [1, 2, 3] #Khoảng trắng bên trái của ký tự "[" là khoảng trắng theo sau của dấu = (chứ không phải là khoảng trắng đặt trước của ký tự "[")

[1, 2, 3].each{ |num| puts num * 2 }

def method(a, b, c)
end
```

- Đặt khoảng trắng vào sau các đối số

```
# Cách viết đúng
arr.each{ |elem| puts elem }

# Cách viết không đúng
arr.each{|elem|puts elem}
```

- Sử dụng here document với chuỗi string dài có bao gồm xuống dòng. Tuy nhiên, cho phép sử dụng string literal khi định nghĩa đoạn message ngắn hoặc dùng method chain.

```
# good
  foo = <<-EOS
    From this valley they say you are going,
    We will miss your bright eyes and sweet smile,
    For they say you are taking the sunshine
    That has brightened our pathways a while.
  EOS

  # ok
    foo = "Hi, Amana.
    How are you?"

  # bad
    foo = "From this valley they say you are going,\nWe will miss your bright eyes and sweet smile,\nFor they say you are taking the sunshine\nThat has brightened our pathways a while."
```

- Hash về cơ bản được viết theo quy ước viết tắt của phiên bản 1.9
```
# Cách viết không đúng
h = {:key => :value}

# Cách viết đúng
h = { key: :value }
```

- Giữa do và đối số đặt 1 khoảng trắng

```
# Cách viết đúng
arr.each do |elem|
  puts elem
end

# Cách viết không đúng
arr.each do|elem|
  puts elem
end
```

- Để lề của when và case như nhau
```
case
when song.name == 'Misty'
  puts 'Not again!'
when song.duration > 120
  puts 'Too long!'
when Time.now.hour > 21
  puts "It's too late"
else
  song.play
end
```

- Tuy nhiên, trong trường hợp ở bên trái của case có gì đó, thì indent của dòng có when lùi vào một khoảng so với dòng của case.

```
foo = case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts “It's too late”
  else
    song.play
  end
```

- Sau một def (method), phải cách nhau một line (khoảng trắng)
```
def method1
  # some proccesses
end

def some_method2
  # some proccesses
end
```

## Các tiêu chuẩn về ngữ pháp
- Không thêm ngoặc `()` trong cách trường hợp method không có params
```
# good
def load_users
...
end

#bad
def load_users()
end
```

- Trường hợp method có params thì bắt buộc phải thêm ngoặc

```
def load_users_by_month(params_1, params_2, ...)
end
```

- Không được dùng `for`

```
arr = [1, 2, 3]

# Cách viết không đúng
for elem in arr do
  puts elem
end

# Cách viết đúng
arr.each{|elem| puts elem}
```

- Không được dùng `then` in if/else, được sử dụng `then` trong `case when` khi thực thi ngắn.
```
# Cách viết không đúng
if some_condition then
  # some proccesses
end

# Cách viết đúng
if some_condition
  # some proccesses
end
```

- Khi sử dụng toán tử 3 điều kiện （ ? : ）, phải viết tất cả các thành phần lệnh trên 1 dòng và trong trường hợp này không dùng if then else
```
# Cách viết đúng
weather = sun.shiny? ? 'well' : 'cloud'

# Cách viết không đúng
weather = sun.shin? ?
  'well'
  :
  'cloud'

# Cách viết không đúng
weather = if sun.shiny? then 'well' else 'cloud' end # you must also not use 'then' keyword.
```

- Không được sử dụng các toán tử 3 điều kiện lồng nhau
```
# Cách viết không đúng
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

# Cách viết đúng
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
```

- Khi có thể dùng && và || thay thế and và or thì nên dùng.

- `if 〜 end` hoặc `unless 〜 end` có thể được giản lược bằng cách đặt if hoặc unless xuống cuối câu.

- Sử dụng thể giản lược khi có thể viết câu trên cùng 1 dòng tối đa 125 ký tự.
```
# Cách viết không đúng
if some_condition
  foo = 'This is a short string'
end

# Cách viết đúng
foo = 'This is a short string' if some_condition

# Cách viết không đúng
foo = "This is a very very long string that can not be broken down and may contain #{variable}" unless some_condition

# Cách viết đúng
unless some_condition
  foo = "This is a very very long string that can not be broken down and may contain #{variable}"
end
```

- Không được dùng unless với else
```
# Cách viết không đúng
unless success?
  puts 'failure'
else
  puts 'success'
end

# Cách viết đúng
if success?
  puts 'success'
else
  puts 'failure'
end
```

- Không sử dụng phép toán phủ định ! trong câu điều kiện if (nếu cần thiết thì dùng unless). Thế nhưng chúng ta vẫn có thể dùng trong trường hợp kết hợp với && hoặc ||. Trong những trường hợp này chúng ta có thể áp dụng các luật De Morgan để viết đơn giản hơn.

```
# cách viết không tốt
if !user.nil?
  user.greeting
end

# cách viết tốt
unless user.nil?
  user.greeting
end

# cách viết rất tốt
if user
  user.greeting
end

# cách viết rất tốt
user.greeting if user

# OK
if !user.nil? && !user.suspended?
  user.greeting
end

# cách viết không tồi nhưng mà hơi phức tạp
unless user.nil? || user.suspended?
  user.greeting
end

# nên viết thế này
if user && user.active?
  user.greeting
end
````

- Không đặt dấu () trong các điều kiện của các lệnh if/unless/while
```
# Cách viết không đúng
if (x > 10)
  # body omitted
end

# Cách viết đúng
if x > 10
  # body omitted
end
```

- Nếu có 1 lệnh block thì dùng{} và viết trên 1 dòng. Trường hợp có nhiều lệnh gộp thì dùng do 〜 end Rule này cũng áp dụng cho trường hợp method chain.

```
names = %w(Bozhidar Steve Sarah)

# Cách viết đúng
names.each{|name| puts name}

# Cách viết không đúng
names.each do |name|
  puts name
end

# Cách viết đúng
[1, 2, 3].map{|num| num * 2}.reduce{|double, sum| sum += double}

# also good
[1, 2, 3].map do |num|
  num * 2
end.reduce do |double, sum|
  sum += double
end
```

- Trong trường hợp có thể bỏ được return thì bỏ
```
# Cách viết không đúng
def some_method(some_arr)
  return some_arr.size
end

# Cách viết đúng
def some_method(some_arr)
  some_arr.size
end
```

- Trong trường hợp có phép gán trong biểu thức điều kiện if thì sử dụng dấu ()
```
# Cách viết đúng
if (v = array.grep(/foo/)) ...

# Cách viết không đúng
if v = array.grep(/foo/) ...

# Cách viết cũng đúng - theo đúng thứ tự ưu tiên
if (v = next_value) == 'hello' ...
```

### Lý do

 - Để tránh nhầm lẫn với method ==

  - Khuyến khích sử dụng cách khởi tạo biến ||=. Tuy nhiên, với biến boolean, cần chú ý là giá trị false sẽ bị ghi đè

```
# Thiết lập name là Bozhidar, chỉ khi name là nil hoặc false
name ||= 'Bozhidar'

# Cách viết không đúng - sẽ set enabled là true ngay cả khi nó là false
enabled ||= true

# Cách viết đúng
enabled = true if enabled.nil?
```

- Giữa tên của method và đối số, không chèn khoảng trắng
```
# Cách viết không đúng
f (3 + 2) + 1

# Cách viết đúng
f(3 + 2) + 1
```

- Không dùng đối số trong block, dùng _
```
# Cách viết không đúng
result = hash.map {|k, v| v + 1}

# Cách viết đúng
result = hash.map { |_, v| v + 1 }
```

- Dùng từ tối giản của tên đối số để đặt tên cho đối số tạm thời trong block, nhưng từ phải thông dụng và dễ hiểu.
```
# Cách viết đúng
products.each {|product| product.maintain!}

# OK
products.each {|prod| prod.maintain!}
```
- Trong trường hợp tạo biến số như Mảng rỗng hay Hash rỗng thì dùng Array.new, Hash.new.

```
# Cách viết không đúng
  @users = []

# Cách viết đúng
  @users = Array.new

# Cũng đúng
  @months_of_birth_date = User.all.inject([]){|months, user| months << user.birth_date.month}
```

### Lý do
  - Thể hiện rõ ý đồ tạo object mới, nên nhìn vào dễ hiểu hơn.

## Cách đặt tên
- Tên method hoặc biến số thì dùng snake_case
- Tên class hoặc module thì dùng CamelCase
- Hằng số tổng quát dùng SCREAMING_SNAKE_CASE
- Các method trả về giá trị boolean thì thêm dấu ? ở cuối như Array#empty?
- Các method hủy hoặc method nguy hiểm thì đặt `!` ở cuối như Array#flatten! Khi định nghĩa method hủy, method không hủy như Array#flatten cũng được định nghĩa.
- Ngoài ra cách method nào làm thay đổi giá trị gốc của đối tượng hoặc raise ra Exception thì phải đặt `!`
## Cách quy định trong Class
- Trách sử dụng biến class @@ trừ khi thực sự cần thiết
```
class Parent
  @@class_var = 'parent'

  def self.print_class_var
    puts @@class_var
  end
end

class Child < Parent
  @@class_var = 'child'
end

Parent.print_class_var # => sẽ hiển thị "child"
```

- Kiểm tra xem biến class instance có thực hiện được không ?
```
class Parent
  @class_instance_var = 'parent'

  def self.print_class_instance_var
    puts @class_instance_var
  end
end

class Child < Parent
  @class_instance_var = 'child'
end

Parent.print_class_var # => sẽ hiển thị "parent"
```

- Khi định nghĩa singleton method (class method), không dùng def self.method hoặc def ClassName.method
```
class TestClass
  # Cách viết không đúng
  def TestClass.some_method
    # body omitted
  end

  # Cách viết không đúng
  def self.some_other_method
    # body omitted
  end
end
```

- Khi định nghĩa 1 method hoặc một class macro cụ thể, dùng class << self
```
class TestClass
  class << self
    attr_accessor :per_page
    alias_method :nwo, :find_by_name_with_owner

    def find_by_name_with_owner
      # body omitted
    end

    def first_method
      # body omitted
    end

    def second_method_etc
      # body omitted
    end
  end
end
```

- Với block những public methods, thì ko cần khai báo public ở trước như cách làm với các block private/protected bên dưới.

- Viết protected methods trước private methods. Lúc đó, khi định nghĩa các protected, private method, căn lề trùng với public method và đặt dòng trắng trên các protected, private methods này, không đặt dòng trắng ở bên dưới.

```
class SomeClass
  def public_method
    # ...
  end

  protected
  def protected_method
    # ...
  end

  private
  def private_method
    # ...
  end
end
```