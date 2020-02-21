C#コーディングスタンダード
------------
  
  
  
Preface
------
Rule of Thumb
----------
1.	Readability first (your code should be your documentation most of the time)
2.	Follow IDE's auto formatted style unless you have really good reasons not to do so. (Ctrl + K + D in Visual Studio)
3.	Learn from existing code



References
---------
This coding standards is inspired by these coding standards
●	Unreal engine 4 coding standard
●	Doom 3 Code Style Conventions
●	IDesign C# Coding Standard
  
  
IDE Helper
-------
The settings that can imported into your IDE can be found here.
I. Naming Conventions and Style
1.	Use Pascal casing for class and structs
class PlayerManager;
struct PlayerData;

2.	Use camel casing for local variable names and function parameters
public void SomeMethod(int someParameter)
{
  int someNumber;
}

3.	Use verb-object pairs for method names

public uint GetAge()
{
  // function implementation...
}

4.	Use pascal casing for all method names except (see below)

public uint GetAge()
{
  // function implementation...
}

5.	Use camel case for any non-public method. You might need to add custom Visual Studio style rule as described here

private uint getAge()
{
  // function implementation...
}

6.	Use ALL_CAPS_SEPARATED_BY_UNDERSCORE for constants
const int SOME_CONSTANT = 1;

7.	Use static readonly if object is a constant

public static readonly MY_CONST_OBJECT = new MyConstClass();

8.	Use ALL_CAPS_SEPARATED_BY_UNDERSCORE for static readonly variables

9.	Use readonly when a variable must be assigned only once

public class Account
{
    private readonly string mPassword;

    public Account(string password)
    {
        mPassword = password;
    }
}

10.	Use pascal casing for namespaces  
 namespace System.Graphics

11.	prefix boolean variables with b and prefix boolean properties with Is  
bool bFired;	// for local variable
private bool mbFired;	// for private member variable
public bool IsFired { get; private set; }	// for property

12.	prefix interfaces with I  
interface ISomeInterface;

13.	prefix enums with E  
public enum EDirection
{
  North,
  South
}

14.	prefix private member variables with m. Use Pascal casing for the rest of a member variable  
Public class Employee
{
  public int DepartmentID { get; set; }
  private int mAge;
}
15.	Methods with return values must have a name describing the value returned  
public uint GetAge();

16.	Use descriptive variable names. e.g index or employee instead of i or e unless it is a trivial index variable used for loops.  

17.	Capitalize every characters in acronyms only if there is no extra word after them.  
public int OrderID { get; private set; }  
public string HttpAddress { get; private set; }    
  
18.	Prefer properties over getter setter functions  
Use:  
public class Employee  
{  
  public string Name {get; set;}  
}  
Instead of:  
public class Employee  
{  
  private string mName;  
  public string GetName();  
  public string SetName(string name);  
}  
  
19.	Use Visual Studio's default for tabs. If another IDE is used, use 4 spaces instead of a real tab.  
  
20.	Declare local variables as close as possible to the first line where it is being used.  
  
21.	Always place an opening curly brace ({) in a new line  
  
22.	Add curly braces even if there's only one line in the scope  
if (bSomething)  
{  
  return;  
}  
  
23.	Use precision specification for floating point values unless there is an explicit need for a double.  
float f = 0.5F;  
  
24.	Always have a default: case for a switch statement.  
switch (number)  
{  
  case 0:  
    ...   
    break;  
  default:  
    break;  
  
  
25.	If default: case must not happen in a switch case, always add Debug.Assert(false); or Debug.Fail();  
switch (type)  
{  
  case 1:  
    ...   
    break;  
  default:  
    Debug.Fail("unknown type");  
    break;  
}  
  
26.	Names of recursive functions end with Recursive  
public void FibonacciRecursive();  
  
27.	Order of class variables and methods must be as follows:  
a.	public variables/properties  
b.	internal variables/properties  
c.	protected variables/properties  
d.	private variables  
i.	Exception: if a private variable is accessed by a property, it should appear right before the mapped property.  
e.	constructors  
f.	public methods  
g.	Internal methods  
h.	protected methods  
i.	private methods  
  
  
28.	Function overloading must be avoided in most cases  
Use:  
public Anim GetAnimByIndex(int index);  
public Anim GetAnimByName(string name);  
  
Instead of:  
public Anim GetAnim(int index);  
public Anim GetAnim(string name);  
  
29.	Each class must be in a separate source file unless it makes sense to group several smaller classes.  
  
30.	The filename must be the same as the name of the class including upper and lower cases.  
public class PlayerAnimation {}  
  
PlayerAnimation.cs  
  
31.	When a class spans across multiple files(i.e. partial classes), these files have a name that starts with the name of the class,   followed by a dot and the subsection name.  
public partial class Human;  
  
Human.Head.cs  
Human.Body.cs  
Human.Arm.cs  
  
32.	Use assert for any assertion you have. Assert is not recoverable. (e.g, most function will have Debug.Assert(not null parameters) )  
  
33.	The name of a bitflag enum must be suffixed by Flags  
public enum EVisibilityFlags  
{  
}  
  
34.	Prefer overloading over default parameters  
  
35.	When default parameters are used, restrict them to natural immutable constants such as null, false or 0.  
  
36.	Shadowed variables are not allowed.  
  
public class SomeClass  
{  
  public int Count { get; set; }  
  public void Func(int count)  
  {  
    for (int count = 0; count != 10; ++count)  
    {  
      // Use count  
    }  
  }  
}  
37.	Always use containers from System.Collections.Generic over ones from System.Collections. Using pure array is fine as well.  
  
38.	Prefer to use real type over implicit typing(i.e, var) unless the type is obvious from the right side of assignment, or when the type is unimportant. Some acceptable var usage includes IEnumerable and when new keyword is on the same line, showing what type of object is being created clearly.  
  
var text = "string obviously";  
var age = 28;  
var employee = new Employee();  
  
string accountNumber = GetAccountNumber();  

39.	Use static class, not singleton pattern  

40.	Use async Task instead of async void. The only place where async void is allowed is for event handler.  

41.	Validate any external data at the boundary and return before passing the data into our functions. This means that we assume all data is valid after this point.  

42.	Therefore, do not throw any exception from inside our function. This should be handled at the boundary only.  

43.	As an exception to the previous rule, exception throwing is allowed when switch-default is used to catch missing enum handling logic. Still, do not catch this exception  
  
switch (accountType)  
{  
  case AccountType.Personal:  
    return something;  
  case AccountType.Business:  
    return somethingElse;  
  default:  
    throw new ArgumentOutOfRangeException(nameof(AccountType));  
}  
  
44.	Prefer not to allow null parameter in your function, especially from a public one.  
  
45.	If null parameter is used, and postfix the parameter name with OrNull  
  
public Anim GetAnim(string nameOrNull)  
{  
}  

46.	Prefer not to return null from any function, especially from a public one. However, you sometimes need to do this to avoid throwing exceptions.  

47.	If null is returned from any function. Postfix the function name with OrNull.  

public string GetNameOrNull();  

48.	Try not to use object initializer. Use explicit constructor with named parameters instead. Two exceptions.  
a.	When the object is created at one place only. (e.g, one-time DTO)  
b.	When the object is created inside a static method of the owning class. (e.g, factory pattern)  

49.	Declare only one variable per line  
BAD:  
int counter = 0, index = 0;  
 
GOOD:   
int counter = 0;  
int index = 0;  

