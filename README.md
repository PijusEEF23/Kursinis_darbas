1. Introduction
     The goal of this coursework is to design and implement a converter that can convert between Roman and decimal numbers.
  a. The application is a converter that can convert Roman numbers to decimal and vice versa. It uses a JSON file to map Roman symbols to their corresponding decimal values.
  b. To run the program, you need to have Python installed on your system. You can run the program by executing the Python script in a terminal or command prompt (a JSON file with parameters is also needed).
  c. To convert Roman numbers to decimal, we need to put Roman symbol between (' '). Example - Code line: "print(decorated_converter.convert('X'))".
     To convert decimal numbers to Roman, we need to put decimal numbers between ( ). Example - Code line: "print(decorated_converter.convert(10))"

_____________________________________________________________________________________________________________________________________________________________________________________________________________________

2. Body/Analysis
  a. The program implements functional requirements through several classes.
     2.1. Converter Class The Converter class is the base class for all converters. It defines the interface that all converters must implement. This includes a convert method that takes an input and returns an output. However, the convert method in the Converter class does nothing, as it’s meant to be overridden by subclasses.
      
class Converter:
    def __init__(self):
        pass

    def convert(self, input):
        pass
   
      2.2. RomanDecimalConverter Class The RomanDecimalConverter class extends the Converter class and implements the conversion between Roman and decimal numbers. It overrides the convert method to provide the actual conversion logic. The class also includes helper methods roman_to_decimal and decimal_to_roman for the respective conversions.

class RomanDecimalConverter(Converter):
    def __init__(self, parameter_file):
        super().__init__()
        with open(parameter_file, 'r') as f:
            parameters = json.load(f)
        self.roman_to_decimal_map = parameters['roman_to_decimal_map']
        self.values = parameters['values']
        self.symbols = parameters['symbols']

    def convert(self, input):
        if isinstance(input, int):
            return self.decimal_to_roman(input)
        elif isinstance(input, str):
            return self.roman_to_decimal(input)

        2.3 ConverterFactory Class The ConverterFactory class is used to create instances of converters. It has a create_converter method that takes the type of converter to create and a parameter file. This design allows for the creation of different types of converters, meeting the requirement for flexibility and extensibility.    

class ConverterFactory:
    def create_converter(self, type, parameter_file):
        if type == 'RomanDecimal':
            return RomanDecimalConverter(parameter_file)

         2.4 ConverterDecorator Class The ConverterDecorator class is used to add additional behavior to the converters. It also extends the Converter class and overrides the convert method. Before and after calling the convert method on the decorated converter, it prints messages to the console. This meets the requirement for adding new behaviors to the converters.

class ConverterDecorator(Converter):
    def __init__(self, converter):
        self.converter = converter

    def convert(self, input):
        print("Converting...")
        result = self.converter.convert(input)
        print("Conversion complete!")
        return result

_________________________________________________________________________________________________________________________________________________________________________________________________________________________________

3. Results and Summary
  a. The program successfully implements a converter that can convert between Roman and decimal numbers. This meets the primary objective of the coursework.

One of the challenges faced during the implementation was handling the subtraction rule in Roman numerals (e.g., IV for 4). This was addressed by checking if the current Roman numeral is less than the next one, and if so, subtracting it from the next one.

Another challenge was designing the program to be flexible and extensible. This was achieved by using the Factory and Decorator design patterns, which allow for the creation of different types of converters and the addition of new behaviors to the converters.

The program includes a comprehensive set of unit tests, ensuring the correctness of the conversions. Writing these tests was crucial for verifying the functionality of the program.

The use of a JSON file for storing the mappings of Roman to decimal numbers adds flexibility to the program, as the mappings can be easily updated or extended without changing the code. However, it also adds a dependency on the file’s presence and correct format, which had to be carefully managed.

  b. This work has resulted in a robust, flexible, and extensible converter program that meets the defined objectives and functional requirements. It demonstrates good software design principles and practices, and it provides a strong foundation for future enhancements and extensions. The program is ready for use and further development.

  c. The application could be extended by adding more types of converters. For example, a converter for binary and decimal numbers could be added. The future prospects of the program include its use in a wide range of applications that require conversion between different number systems.
