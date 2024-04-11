# Object-Oriented Programming With C++

    #include <iostream>
	using std::string;
	
	class AbstractEmployee {
	    // virtual is used to make it obligatory
	    virtual void AskForPromotion() = 0;
	};

	class Employee:AbstractEmployee {
	// useful for encapsulation, as in this way you can access the Intro, but not the values
	private:
	    string Company;
	    int Age;
    // so the child can use it
    protected:
        string Name;
    public:
        // to publicly access the encapsulated values
        void setName(string name) {
            Name = name;
        }
        string getName() {
            return Name;
        }
        
        void setCompany(string company) {
            Company = company;
        }
        string getCompany() {
            return Company;
        }
    
        void setAge(int age) {
            // also, you can even put conditions
            if (age >= 35) {
                Age = age;
            }
        }
        int getAge() {
            return Age;
        }
    
    
        void Intro() {
            std::cout << Name << " " << Company << " " << Age << std::endl;
        }
        
        // rules and consequences of constructors: 
        // 1. it does not have a return type
        // 2. it should be the same name as the class
        // 3. it needs to be public
        Employee(string name, string company, int age) {
            Name = name;
            Company = company;
            Age = age;
        }
        
        // if we do not make this function, we will get errors because this is a virtual function
        void AskForPromotion() {
            if (Age > 45) {
                std::cout << Name << " is promoted." << std::endl;
            }
            else {
                std::cout << "Nope, no promotion yet." << std::endl;
            }
        }
        
        // putting "virtual" here makes sure if the derived class has the same function (a.k.a polymorphism)
        // then run the derived function instead
        virtual void Work() {
            std::cout << "Works for Mother Russia!" << std::endl;
        }
    };
    
    // this is the "child" of Employee
    // "public" is used so the abstract class can be used by the child
    class Developer:public Employee {
    public:
        // the value is not encapsulated here (matter of choice)
        string ProgrammingLanguage;
    
        // we have to necessarily provide a constructor because the "parent" has its own
        Developer(string name, string company, int age, string programmingLanguage)
            // a shortcut, instead of writing it all over again
            :Employee(name, company, age)
        {
            ProgrammingLanguage = programmingLanguage;
        }
        
        // now you can do whatever you want
        void Work() {
            std::cout << "Fixes coding problems for stone-age people." << std::endl;
        }
    };
    
    int main()
    {
        Employee employee1 = Employee("Peter Griffin", "Comedy", 41);
        // use this when you have not made your own constructor
        // employee1.Name = "Peter Griffin";
        // employee1.Company = "Comedy";
        // employee1.Age = 41;
        employee1.Intro();
        
        employee1.setAge(46);
        std::cout << employee1.getName() << " is " << employee1.getAge() << std::endl;
        employee1.AskForPromotion();
        
        Developer d = Developer("Tech", "Bad Batch", 25, "Python");
        // used in the case of polymorphism, so things become easy
        Employee* employee2 = &d;
        employee2->Work();
    
        return 0;
    }

