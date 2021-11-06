# ProgrammingWidgetLayout

## INTRODUCTION
The goal of this applications is to get familiar with widgets and layouts and to know how to work with them.  
In the following applications we're going to use various qt classes and widgets so first we're going to give a small definition about each one.  

**-QWidget :** The QWidget class is the base class of all user interface objects it provides a set of UI elements to create classic desktop-style user interfaces.  
**-QLabel :** The QLabel widget provides a text or image display.No user interaction functionality is provided. The visual appearance of the label can be configured in various ways, and it can be used for specifying a focus mnemonic key for another widget.  
**-QLineEdit :** The QLineEdit widget is a one-line text editor.A line edit allows the user to enter and edit a single line of plain text with a useful collection of editing functions, including undo and redo, cut and paste, and drag and drop.  
**-QPushButton:** The QPushButton widget provides a command button.The push button, or command button, is perhaps the most commonly used widget in any graphical user interface. Push (click) a button to command the computer to perform some action, or to answer a question.   
**-QTextEdit :** The QTextEdit class provides a widget supporting rich text formatting using HTML-style tags, or Markdown format. It is optimized to handle large documents and to respond quickly to user input.    
**-QComboBox :** The QComboBox widget is a combined button and popup list.It is a selection widget that displays the current item, and can pop up a list of selectable items. A combobox may be editable, allowing the user to modify each item in the list.   
**-QCheckBox :** A QCheckBox is an option button that can be switched on (checked) or off (unchecked).  
**-QDiialogButtonBox :** The QDialogButtonBox class is a widget that presents buttons in a layout that is appropriate to the current widget style.    
**-QFormLayout :** The QFormLayout is a convenience layout class that lays out its children in a two-column form. The left column consists of labels and the right column consists of "field" widgets (line editors, spin boxes, etc.).The addRow() overload that takes a QString and a QWidget * creates a QLabel behind the scenes and automatically set up its buddy.   
**-QFormLayout :** The QBoxLayout class lines up child widgets horizontally or vertically.  
**-QVBoxLayout :** The QVBoxLayout class lines up widgets vertically.  
**-QHboxLayout :** The QHBoxLayout class lines up widgets horizantally.  
**-QLCDNumber :** The QLCDNumber widget displays a number with LCD-like digits.  
**-QGridLayout :** The QGridLayout takes the space made available to it (by its parent layout or by the parentWidget()), divides it up into rows and columns, and puts each widget it manages into the correct cell. We will us the method with the folllowing syntax:  
**void QGridLayout::addWidget(QWidget *widget, int row, int column, Qt::Alignment alignment = Qt::Alignment())*** which adds the given widget to the cell grid at row, column. The top-left position is (0, 0) by default.The alignment is specified by alignment. The default alignment is 0, which means that the widget fills the entire cell.




## Experimenting with QHBOXLayout
In this first application we will learn to use QHBoxLayout
  ###   .header
  ```cpp
  #ifndef QHBOX_H
#define QHBOX_H

#include<QtWidgets>
#include<QPushButton>
#include<QLineEdit>
#include<QLabel>
#include <QWidget>

class QHbox : public QWidget
{
    Q_OBJECT
public:
    explicit QHbox(QWidget *parent = nullptr);
protected:
   void createwidgets();
   void placewidgets();

protected:
   QLineEdit * edit;
   QLabel * label;
   QPushButton * search;



};

#endif // QHBOX_H

  ```
We first start by declaring the variables and methods we are going to use in the header :createwidgets() for creating the different widgets the placewidgets() method to create the layouts and place every widget in its place.  
### .cpp
```cpp
#include "qhbox.h"

QHbox::QHbox(QWidget *parent) : QWidget(parent)
{// creer les widgets
    createwidgets();



    //les placer
    placewidgets();


}
void QHbox::createwidgets(){
    label= new QLabel("Name :");
    edit= new QLineEdit;
    search= new QPushButton("Search");

}
void QHbox::placewidgets(){
    auto layout = new QHBoxLayout;
    setLayout(layout);

    layout->addWidget(label);
    layout->addWidget(edit);
    layout->addWidget(search);
   setWindowTitle("QHBOXLayout test");
}
```
### main.cpp
```cpp
#include <QApplication>
#include<qhbox.h>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
   QHbox * q= new QHbox;
   q->show();
    return a.exec();
}
```
### Output

## Nested Layouts
In this second application we will learn to analyse the construction of a form and then code it using Netsted layouts.
### .header
```cpp
#ifndef NESTEDLAYOUT_H
#define NESTEDLAYOUT_H

#include <QWidget>
#include<QtWidgets>
#include<QPushButton>
#include<QLineEdit>
#include<QLabel>
#include<QCheckBox>


class NestedLayout : public QWidget
{
    Q_OBJECT
public:
    explicit NestedLayout(QWidget *parent = nullptr);

protected:
   void createwidgets();
   void placewidgets();
   void makeconnections();
protected:
   QLabel * nameLabel;
   QLineEdit * nameEdit;
   QPushButton * search;
   QPushButton * close;
   QCheckBox * match;
   QCheckBox *backwards;


};

#endif // NESTEDLAYOUT_H
```
We used the same methods as the first apllication and we added another which is makeconnections() and that one is to establish connection beetween two widgets or assign to a widget a function to acomplish . The classical connect mecansim looks like:  
connect(sender, SIGNAL(signal), receiver, SLOT(slot));  
### .cpp
```cpp
#include "nestedlayout.h"
#include<QApplication>
NestedLayout::NestedLayout(QWidget *parent) : QWidget(parent)
{
    // creer les widgets
        createwidgets();

        //les placer
        placewidgets();

        //mettre les connections
        makeconnections();
}
void NestedLayout::createwidgets(){
    nameLabel = new QLabel("Name :");
    nameEdit = new QLineEdit;
    search = new QPushButton("Search");
    close  = new QPushButton("Close");
    match = new QCheckBox("Match case");
    backwards = new QCheckBox("Search backwards");

}
void NestedLayout::placewidgets(){
    auto mainlayout = new QHBoxLayout;
    auto rightlayout =new QVBoxLayout;
    auto topleftlayout = new QHBoxLayout;
    auto leftlayout = new QVBoxLayout;

 setLayout(mainlayout);

  mainlayout->addLayout(leftlayout);
  mainlayout->addLayout(rightlayout);

  leftlayout->addLayout(topleftlayout);

  topleftlayout->addWidget(nameLabel);
  topleftlayout->addWidget(nameEdit);

  leftlayout->addWidget(match);
  leftlayout->addWidget(backwards);

  rightlayout->addWidget(search);
  rightlayout->addWidget(close);
  rightlayout->addSpacerItem(new QSpacerItem(10,10,QSizePolicy::Expanding));

  setWindowTitle("Nested Layout Test");



}
void NestedLayout::makeconnections(){
    connect(close,&QPushButton::clicked,qApp,&QApplication::exit);
}
```
### main.cpp
```cpp
#include <QApplication>
#include<nestedlayout.h>
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    NestedLayout * N =new NestedLayout;
    N->show();

    return a.exec();
}
```
### Output

## Bug report Form
Our task in this third application is to create a DialogBox to report a problem.
### .header
```cpp
#ifndef BUGFORM_H
#define BUGFORM_H
#include<QLineEdit>
#include<QTextEdit>
#include<QComboBox>
#include<QDialogButtonBox>

#include <QWidget>

class BugForm : public QWidget
{
    Q_OBJECT
public:
    explicit BugForm(QWidget *parent = nullptr);

protected:
   void createwidgets();
   void placewidgets();




private:
           QLineEdit *nameEdit;
           QLineEdit *companyEdit;
           QLineEdit *phoneEdit;
           QLineEdit *emailEdit;
           QLineEdit *problemEdit;
           QTextEdit *summaryEdit;
           QComboBox *reproducibilityCombo;
           QDialogButtonBox *buttonBox;

};

#endif // BUGFORM_H
```
### .cpp
```cpp
#include "bugform.h"
#include<QFormLayout>
#include<QVBoxLayout>

BugForm::BugForm(QWidget *parent) : QWidget(parent)
{  createwidgets();

    placewidgets();



}
void BugForm::createwidgets(){
           nameEdit = new QLineEdit;
           companyEdit = new QLineEdit;
           phoneEdit = new QLineEdit;
           emailEdit = new QLineEdit;
           problemEdit = new QLineEdit;
           summaryEdit = new QTextEdit;

           reproducibilityCombo = new QComboBox;
           reproducibilityCombo->addItem("Always");
           reproducibilityCombo->addItem("Sometimes");
           reproducibilityCombo->addItem("Rarely");

           buttonBox = new QDialogButtonBox;
           buttonBox->addButton(("Submit Bug Report"),
                                QDialogButtonBox::AcceptRole);
           buttonBox->addButton(("Don't Submit"),
                                QDialogButtonBox::RejectRole);
           buttonBox->addButton(QDialogButtonBox::Reset);
}
void BugForm::placewidgets(){
            QFormLayout *layout = new QFormLayout;
            layout->addRow(tr("&Name:"), nameEdit);
            layout->addRow(tr("&Company:"), companyEdit);
            layout->addRow(tr("&Phone:"), phoneEdit);
            layout->addRow(tr("&Email:"), emailEdit);
            layout->addRow(tr("Problem &Title:"), problemEdit);
            layout->addRow(tr("&Summary Information:"),
                           summaryEdit);
            layout->addRow(tr("&Reproducibility:"),
                           reproducibilityCombo);

            QVBoxLayout *mainLayout = new QVBoxLayout;
            mainLayout->addLayout(layout);
            mainLayout->addWidget(buttonBox);
            setLayout(mainLayout);

            setWindowTitle(tr("Report Bug"));
}

```
### main.cpp
```cpp
#include <QApplication>
#include<bugform.h>


int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
   BugForm *B=new BugForm;
   B->show();

    return a.exec();
}

```
### Output

## Grid Layout
In this fourth application we will try to create the interface of a simple calculator.
### .header
```cpp
#ifndef CALCULATOR_H
#define CALCULATOR_H

#include <QWidget>
#include<QLineEdit>
#include<QLabel>
#include<QPushButton>
#include<QBoxLayout>
#include<QCheckBox>
#include<QLCDNumber>

class calculator : public QWidget
{
    Q_OBJECT
public:
    explicit calculator(QWidget *parent = nullptr);

protected:
void createwidgets();
void placewidgets();

protected:

QLCDNumber *numero;

  enum { NumDigitButtons = 10 };
  QPushButton *digitButtons[NumDigitButtons];
QPushButton *button;

};

#endif // CALCULATOR_H
```
We have used here enum also called enumeration which is a data type consisting of named values like elements, members, etc., that represent integral constants. It provides a way to define and group integral constants. It also makes the code easy to maintain and less complex.
### .cpp
```cpp
#include "calculator.h"

calculator::calculator(QWidget *parent) : QWidget(parent)
{  createwidgets();
    placewidgets();

}
void calculator::createwidgets(){

   numero=new QLCDNumber;
   //max it can contains 6 digits
    numero->setDigitCount(6);
    //set a minimum height of 80 pixels
   numero->setMinimumHeight(80);


         for (int i = 0; i < NumDigitButtons; ++i) {
             digitButtons[i] = new QPushButton(QString::number(i));
         }
         button=new QPushButton("Enter");
              }



void calculator::placewidgets(){
 QGridLayout *mainLayout = new QGridLayout;
 mainLayout->addWidget(numero, 0, 0, 1,3);


 int z=0;
       for (int i = 4; i >= 1; i--) {
          if(z==10)
           break;
       for (int j = 0; j < 3; j++){
               if(j>0 && i == 4)
                   break;
               else
            mainLayout->addWidget(digitButtons[z], i, j);
             z++;
           }
       }
   mainLayout->addWidget(button, 4, 1, 1, 2);
   this->setLayout(mainLayout);
   setWindowTitle("NumericKeypad");
}

```
### main.cpp
```cpp
#include <QApplication>

#include<calculator.h>
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    calculator * c=new calculator;
    c->show();

    return a.exec();
}

```
### Output

## CONCLUSION
As a summary we have learned how to work with different types of layouts and widgets and how to manipulate them ,in addition we got familiar with a lot of important concepts and classes .Now we are looking forward to learn how to make those forms functional like the example of the calculator .  
    
      
      
  >Team : Aya Benlahbib and Asmae Tnani 





