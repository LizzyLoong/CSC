当一个函数的实参值无意义时要抛出的异常就是这个类型。
这个类C++并没有给出来，需要我们自己实现
```
class illegalParameterValue
{
public:
	illegalParameterValue():message("Illegal parameter value"){}
	illegalParameterValue(char* theMessage) { message = theMessage; }
	void outputMessage() { cout << message << endl; }
private:
	string message;
};
```