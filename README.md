#include"Person.h"
#include"Student.h"
#include"Instructor.h"
#include"E_Course.h"
#include"Classroom.h"
#include"Teams.h"
#include"ManagementSystem.h"
#include<iostream>
using namespace std;
int main() {
	char option;
	Person p;
	Teams* tea = &p;
	tea->ourSystem();
	tea->start();
	p.enterInfo();
	p.displayInfo();
	cout << "**************************LOBBY**********************************" << endl;
	cout << "WAITING IN LOBBY FOR THE INSTRUCTOR TO ADD YOU" << endl;
	cout << "DO YOU WANT TO ADD ANOTHER PERSON?" << endl;
	cin >> option;
	if (option == 'Y' || option == 'y') {
		p.enterInfo();
		p.displayInfo();
	}
	E_Course e;
	e.displayInfo();
	cout << "**************************FUNCTIONALITIES********************************" << endl;
	cout << "****************************INSTRUCTOR*****************************" << endl;
	cout << "FOLLOWING FUNCTIONALITIES ARE ONLY FOR THE INSTRUCTOR:" << endl;
	cout << "1:  ADD STUDENT" << endl;
	cout << "2:  DELETE STUDENT" << endl;
	cout << "3:  CREATE ASSIGNMNET" << endl;
	cout << "4:  ENABLE CAMERA" << endl;
	cout << "5:  DISABLE CAMERA" << endl;
	cout << "6:  MUTE STUDENT" << endl;
	cout << "7:  SCREEN SHARING" << endl;
	cout << "****************************STUDENT*****************************" << endl;
	cout << "FOLLOWING FUNCTIONALITIES ARE ONLY FOR THE STUDENT:" << endl;
	cout << "8:  SUBMIT ASSIGNMNET" << endl;
	cout << "9:  RAISE HAND" << endl;
	cout << "10: LOWER HAND" << endl<<endl;
	Classroom c;
	c.redo();
	char opt;
	cout << "DO YOU WANT TO SWITCH THE PERSON?" << endl;
	cin >> opt;
	if (opt == 'Y' || opt == 'y') {
		c.redo();
	}
	if (opt == 'N' || opt == 'n') {
		cout << "THE END" << endl;
		cout << "************************************************************" << endl;
	}
	return 0;
}
class Teams
{
public:
	virtual void start() = 0;
	void ourSystem();
};
void Teams::ourSystem()
{
	cout << "YOUR SYSTEM HAS BEEN STARTED" << endl;
}
class ManagementSystem
{
	virtual void enterInfo() =0;
	virtual void displayInfo() =0;
};
class Person:public ManagementSystem,public Teams
{
public:
	string name;
	int teamsid;
	virtual void start() override;
	virtual void enterInfo() override;
	virtual void displayInfo() override;
};
void Person::start()
{
	cout << "************************************************************" << endl;
	cout << "**********************WELCOME TO TEAMS**********************" << endl;
}
void Person::enterInfo()
{
	cout << "ENTER YOUR NAME:";
	cin >> name;
	cout << "ENTER YOUR TEAMS ID:";
	cin >> teamsid;
}
void Person::displayInfo()
{
	char choose;
	cout << "*********************************" << endl;
	cout << "YOUR DETAILS INCLUDE: " << endl;
	cout << "NAME: " << name << endl;
	cout << "TEAMS ID: " << teamsid << endl;
	cout << "ARE YOU A STUDENT?" << endl;
	cin >> choose;
	if (choose == 'Y' || choose == 'y') {
		Student s;
		s.enterInfo();
	}
	if (choose == 'N' || choose == 'n') {
		Instructor i;
		i.enterInfo();
	}
}
class Student :
    public Person
{
    public:
    int studentID;
    int password;
    void enterInfo() override;
    void displayInfo() override;
};
void Student::enterInfo()
{   password = 1234;
	cout << "ENTER YOUR STUDENT ID:";
	cin >> studentID;
	cout << "ENTER YOUR PASSWORD:";
	cin >> password;
	if (password == 1234) {
		Student::displayInfo();
	}
	else {
		cout << "     ERROR!!!!!!     " << endl;
		cout << "     WRONG PASSWORD     " << endl;
		cout << "     ENTER AGAIN     " << endl<<endl;
		Student::enterInfo();
	}
}
void Student::displayInfo()
{
	cout << "  STUDENT: " << endl;
	cout << "STUDENT ID: " << studentID << endl;
	cout << "PASSWORD: " << password << endl;
	cout << studentID << " IS PRESENT " << endl<<endl;
}
class Instructor :
    public Person
{
private:
    int instructorID;
    int password_login;
public:
    void enterInfo() override;
    void displayInfo() override;
};
void Instructor::enterInfo()
{
	password_login = 5678;
	cout << "ENTER YOUR INSTRUCTOR ID: ";
	cin >> instructorID;
	cout << "ENTER YOUR PASSWORD: ";
	cin >> password_login;
	if (password_login == 5678) {
		Instructor::displayInfo();
	}
	else {
		cout << "     ERROR!!!!!!     " << endl;
		cout << "     WRONG PASSWORD     " << endl;
		cout << "     ENTER AGAIN     " << endl<<endl;
		Instructor::enterInfo();
	}
}
void Instructor::displayInfo()
{
	cout << "  INSTRUCTOR: " << endl;
	cout << "INSTRUCTOR ID: " << instructorID << endl;
	cout << "PASSWORD: " << password_login << endl;
	cout << instructorID << " IS PRESENT " << endl<<endl;
}
class E_Course :
    public Student,public Instructor
{
public:
    string course;
    string course_code;
    string course_title;
    double schedule;
    int student_strength;
    string assignedInstructor;
    void displayInfo() override;
    void chooseCourse();
};
void E_Course::displayInfo()
{
	cout << "***************************************************" << endl;
	cout << "SCHEDULE" << endl;
	cout << " ------------ -------- ------- " << endl;
	cout << "| DAY        | COURSE | TIME  |" << endl;
	cout << " ------------ -------- ------- " << endl;
	cout << "| MONDAY     | TBW    | 1.10  |" << endl;
	cout << "| TUESDAY    | OOP    | 9.30  |" << endl;
	cout << "| WEDNESDAY  | DLD    | 8.45  |" << endl;
	cout << "| THURSDAY   | VC     | 2.00  |" << endl;
	cout << "| FRIDAY     | THERMO | 11.25 |" << endl;
	cout << " ------------ -------- ------- " << endl;
}
	void E_Course::chooseCourse()
	{
	cout << "ENTER YOUR COURSE TO GET DETAILS ABOUT SCHEDULED CLASS" << endl;
	cin >> course;
	if(course=="TBW"){
		course_title = "TBW";
		course_code = "HU-102";
		schedule = 1.10;
		student_strength = 44;
		assignedInstructor = "DR.MARIA";
		cout << "************************************************" << endl;
		cout << "THE DETAILS ABOUT YOUR SCHEDULED CLASS ARE:" << endl;
		cout << "COURSE TITLE: " << course_title << endl;
		cout << "COURSE CODE: " << course_code << endl;
		cout << "SCHEDULED CLASS: " << schedule << endl;
		cout << "ENROLLED STUDENTS: " << student_strength << endl;
		cout << "ASSIGNED INSTRUCTOR: " << assignedInstructor << endl;
	}
	if(course=="OOP"){
		course_title = "OOP";
		course_code = "CS-100";
		schedule = 9.30;
		student_strength = 42;
		assignedInstructor = "DR.ALI_SAEED";
		cout << "************************************************" << endl;
		cout << "THE DETAILS ABOUT YOUR SCHEDULED CLASS ARE:" << endl;
		cout << "COURSE TITLE: " << course_title << endl;
		cout << "COURSE CODE: " << course_code << endl;
		cout << "SCHEDULED CLASS: " << schedule << endl;
		cout << "ENROLLED STUDENTS: " << student_strength << endl;
		cout << "ASSIGNED INSTRUCTOR: " << assignedInstructor << endl;

	}
	if (course == "DLD") {
		course_title = "DLD";
		course_code = "EE-201";
		schedule = 8.45;
		student_strength = 45;
		assignedInstructor = "DR.MAHRUKH_LIAQUAT";
		cout << "************************************************" << endl;
		cout << "THE DETAILS ABOUT YOUR SCHEDULED CLASS ARE:" << endl;
		cout << "COURSE TITLE: " << course_title << endl;
		cout << "COURSE CODE: " << course_code << endl;
		cout << "SCHEDULED CLASS: " << schedule << endl;
		cout << "ENROLLED STUDENTS: " << student_strength << endl;
		cout << "ASSIGNED INSTRUCTOR: " << assignedInstructor << endl;

	}
	if (course == "VC") {
		course_title = "VC";
		course_code = "MATH-211";
		schedule = 2.00;
		student_strength = 41;
		assignedInstructor = "DR.YASIR_ALI";
		cout << "************************************************" << endl;
		cout << "THE DETAILS ABOUT YOUR SCHEDULED CLASS ARE:" << endl;
		cout << "COURSE TITLE: " << course_title << endl;
		cout << "COURSE CODE: " << course_code << endl;
		cout << "SCHEDULED CLASS: " << schedule << endl;
		cout << "ENROLLED STUDENTS: " << student_strength << endl;
		cout << "ASSIGNED INSTRUCTOR: " << assignedInstructor << endl;

	}
	if (course == "THERMO") {
		course_title = "THERMO";
		course_code = "ME-204";
		schedule = 11.25;
		student_strength = 45;
		assignedInstructor = "DR.SALMAN";
		cout << "************************************************" << endl;
		cout << "THE DETAILS ABOUT YOUR SCHEDULED CLASS ARE:" << endl;
		cout << "COURSE TITLE: " << course_title << endl;
		cout << "COURSE CODE: " << course_code << endl;
		cout << "SCHEDULED CLASS: " << schedule << endl;
		cout << "ENROLLED STUDENTS: " << student_strength << endl;
		cout << "ASSIGNED INSTRUCTOR: " << assignedInstructor << endl;

	}
	else
		cout << "INVALID COURSE" << endl;
	E_Course cour;
	cour.chooseCourse();

}
class Classroom final :public E_Course
{
public:
	int StuId;
	int id;
	void instructor_functionality();
	void student_functionality();
	void select_inst_func();
	void select_stu_func();
	void addStudent();
	void removeStudent();
	void create_assignment();
	void submit_assignment();
	void mute();
	void enable_camera();
	void disable_camera();
	void screensharing();
	void raisehand();
	void lowerhand();
	void redo();
};
void Classroom::instructor_functionality()
{   int inst_password;
	cout << "ENTER INSTRUCTOR PASSWORD TO GET ACCESS" << endl;
	cout << "PASSWORD ";
	cin >> inst_password;
	if (inst_password == 1919) {
		cout << "YOU HAVE GOT THE ACCESS" << endl<<endl;
	}
	else {
		cout << "INCORRECT PASSWORD" << endl;
		cout << "ENTER VALID PASSWORD" << endl<<endl;
		Classroom cls;
		cls.instructor_functionality();
	}
}

void Classroom::student_functionality()
{
	cout << "ENTER YOUR STUDENT ID TO GET ACCESS"<<endl;
	cin >> id;
	cout << "YOU HAVE GOT THE ACCESS" << endl << endl;
}

void Classroom::select_inst_func()
{
	Classroom cls;
	int number;
	cout << "ENTER THE NUMBER FROM 1-7 TO PERFORM SPECIFIC FUNCTION" << endl;
	cin >> number;
	if (number == 1)
		cls.addStudent();
	if (number == 2)
		cls.removeStudent();
	if (number == 3)
		cls.create_assignment();
	if (number == 4)
		cls.enable_camera();
	if (number == 5)
		cls.disable_camera();
	if (number == 6)
		cls.mute();
	if (number == 7)
		cls.screensharing();
	if (number < 1 || number>7) {
		cout << "INVALID INPUT" << endl;
	}
	char another;
	cout << "DO YOU WANT TO PERFORM ANOTHER FUNCTION?" << endl;
	cin >> another;
	if (another == 'Y' || another == 'y')
		cls.select_inst_func();
	else
		exit;
}
void Classroom::select_stu_func()
{
	Classroom cls;
	int no;
	cout << "ENTER THE NUMBER FROM 8-10 TO PERFORM SPECIFIC FUNCTION" << endl;
	cin >> no;
	if (no == 8)
		cls.submit_assignment();
	if (no == 9)
		cls.raisehand();
	if (no == 10)
		cls.lowerhand();
	if (no<8 || no>10){
		cout << "INVALID INPUT" << endl;
	}
	char other;
	cout << "DO YOU WANT TO PERFORM ANOTHER FUNCTION?" << endl;
	cin >> other;
	if (other == 'Y' || other == 'y')
		cls.select_stu_func();
	else
		exit;
	}

void Classroom::addStudent()
{
	cout << "ADD STUDENT " << endl;
	Student stu;
	stu.enterInfo();
	stu.displayInfo();
}

void Classroom::removeStudent()
{
	cout << "REMOVE STUDENT " << endl;
	cout << "ENTER STUDENT ID ";
	cin >> StuId;
	cout << "STUDENT WITH ID " << StuId << " HAS BEEN REMOVED" << endl;
	Student* StuId = new Student();
	delete StuId;
}

void Classroom::create_assignment()
{
	int deadline;
	cout << " ASSIGNMENT " << endl;
	cout << "CREATE ASSIGNMENT?";
	cout << "UPLOAD THE FILE HERE" << endl;
	cout << "ENTER THE DEADLINE ";
	cin >> deadline;
	cout << "SUBMIT YOUR ASSIGNMENT BEFORE " << deadline << endl;

}

void Classroom::submit_assignment()
{
	cout << "ASSIGNMENT " << endl;
	cout << "SUBMIT ASSIGNMENT" << endl;
	cout << "UPLOAD YOUR FILE HERE" << endl;
}

void Classroom::mute()
{
	cout << "MUTE STUDENT " << endl;
	cout << "ENTER STUDENT ID ";
	cin >> id;
	cout << "STUDENT WITH ID " << id << " HAS BEEN MUTED" << endl;
}

void Classroom::enable_camera()
{
	cout << "ENABLE CAMERA" << endl;
	cout<< "YOUR CAMERA HAS BEEN ENABLED" << endl;
}

void Classroom::disable_camera()
{
	cout << "DISABLE CAMERA" << endl;
	cout << "ENTER STUDENT ID ";
	cin >> id;
	cout << "STUDENT WITH ID " << id << " CAMERA HAS BEEN DISABLED" << endl;
}

void Classroom::screensharing()
{
	char share;
	cout << "SCREEN SHARING" << endl;
	cout << "EITHER SHARE YOUR SCREEN" << endl;
	cout << "OR ENTER STUDENT ID ";
	cin >> id;
	cout << "STUDENT WITH ID " << id << " CAMERA HAS BEEN DISABLED" << endl;
}

void Classroom::raisehand()
{
	cout << "RAISE HAND" << endl;
	cout << "CLICK ON THE ICON TO RAISE HAND" << endl;
	cout << "YOUR HAND HAS BEEN RAISED" << endl;
}

void Classroom::lowerhand()
{
	cout << "LOWER HAND" << endl;
	cout << "YOUR HAND HAS BEEN LOWERED" << endl;
}

void Classroom::redo()
{
	string func;
	cout << "ARE YOU A STUDENT OR A INSTRUCTOR?" << endl;
	cin >> func;
	Classroom cls;
	if (func == "INSTRUCTOR" || func=="instructor") {
	cls.instructor_functionality();
	cls.select_inst_func();
	}
	if (func == "STUDENT" || func=="student") {
	cls.student_functionality();
	cls.select_stu_func();
	}
}
