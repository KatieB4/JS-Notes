# Numbers, Dates, Intl, and Timers

### 6/26/23

- because js (and some other languages, ex php, ruby) operates in binary, base 2, some fractions are difficult to represent and can lead to unexpected math results
![alt](images/12-numbers/2023-06-26-1.png)

- convert strings to numbers with number object constructor or just by putting plus sign in front
![alt](images/12-numbers/2023-06-26-2.png)

#### Number.parseInt
- parseInt will pull a number out of a string, even with spaces, as long as the string starts with the number
- parseInt takes a second parameter, the radix, which is the base of the numeral system (usually 10)
![alt](images/12-numbers/2023-06-26-3.png)

#### Number.parseFloat
- parseInt only pulls out the integer part of a number, while parseFloat pulls the whole number, including decimal
![alt](images/12-numbers/2023-06-26-4.png)

- parseInt and parseFloat are global functions, meaning that they will both work without the Number object constructor specified, but it is better practice to use the number object, which provides a "namespace"

#### Number.isNaN
- isNaN works with number constructor to identify what is and is not a number (NaN)
![alt](images/12-numbers/2023-06-26-5.png)

#### Number.isFinite
- use isFinite can sometimes be better to check if something is or is not a number (instead of a string) because of the idiosyncrasies of isNaN (ex, Infinity
![alt](images/12-numbers/2023-06-26-6.png)

#### Number.isInteger
- isInteger checks if input is an integer number

#### Roots of Numbers
- use sqrt Math method (square root only) or exponentiation to a fractional root to get square, cube, etc roots

#### maximum/ minimum
- Math.max and Math.min will automatically perform type coercion, so that if some of the number inputs are written as strings, they will be automatically converted to numbers for the max/mincalculation
- Math.max/min does not parse numbers from strings that include other characters though
![alt](images/12-numbers/2023-06-26-7.png)

#### Rounding
- Math.trunc simply removes any numbers after decimal point
- Math.round will actually round up or down
- Math.ceil (ceiling) will automatically round up
- Math.floor will automatically round down
- all of these math rounding methods will also automatically do type coercion on string inputs
![alt](images/12-numbers/2023-06-26-8a.png)
- with negatives, trunc still just removes after decimal, but rounding is more negative for floor, and less negative for ceiling
![alt](images/12-numbers/2023-06-26-8b.png)
- toFixed allows you to specify number of decimal places, but returns a string, not a number, so convert to number with number constructor or plus sign
- toFixed converts to a string because it is a primitive and (similar to string methods), and primitives can't have methods, so first it is converted to string via boxing, before performing the operation
![alt](images/12-numbers/2023-06-26-8c.png)

#### Remainder (modulo)
- percentage sign is symbol for remainder operator, returns the remainder only of the division of two numbers
![alt](images/12-numbers/2023-06-26-9.png)

### 6/27/23

#### Numeric Separators
- Numeric separators- underscores(_) (like comma in math) separate numbers, to make the code easier to read, but they are not logged in the console
![alt](images/12-numbers/2023-06-27-1a.png)
- be mindful that because the underscore is not really part of the number and only for ease of reading that regardless of where it is placed, it will really be the same number, even though in one case you might use it like a comma to indicate thousands, and in another like a period to indicate cents
![alt](images/12-numbers/2023-06-27-1b.png)
- numeric separator can only be placed between numbers (ex: not number and decimal, not two in a row, not at beginning, not at end of number)
![alt](images/12-numbers/2023-06-27-1c.png)
-number separate also doesn't work when converting with number object operator- js won't be able to parse the number correctly from the string
- also doesn't work with parseInt because only first part before the underscore will be pulled
![alt](images/12-numbers/2023-06-27-1d.png)

#### BigInt Primitive Data Type 
- 64bit limit: there are 64 0's or 1's to represent any given number
- only 53 bits are allowed for the numerals themselves, the other 11 are for decimals, sign, etc
- because of this, the largest number js can represent is 2 (for 0 or 1- base 2) raised to the 53 power (minus 1 because count starts at 0, not 1
- this information is also stored in the MAX_SAFE_INTEGER in the number static data property
- any integer larger than the max safe integer is not safe, meaning it cannot be accurately represented
![alt](images/12-numbers/2023-06-27-2a.png)
- add an "n" to the end of large numbers to indicate that they are "Bigint"
- or use "BigInt" constructor function to indicate big integer- can be problematic because first js has to interpret the large number before adding n to end
![alt](images/12-numbers/2023-06-27-2b.png)
- BigInt can be combined with other BigInt, but not regluar numbers because the BigInt cannot be converted to a regular number
![alt](images/12-numbers/2023-06-27-2c.png) 
- As a workaround, use the BigInt constructor function on the regular number first
![alt](images/12-numbers/2023-06-27-2d.png) 
- One exception: BigInt and regular numbers can be compared with greater than/ less than comparison operators
- strict equlity comparison operator doesn't work because js doesn't do type coercion, and the regular number and the bigint number are two different primitive types, but they will be equal wit the looser equality operator
![alt](images/12-numbers/2023-06-27-2e.png)
- BingInt can be concatenated into streings.
- Math operations (ex sqrt, rounding, etc) cannot be used with BigInt.
![alt](images/12-numbers/2023-06-27-2f.png)
- Dividing with bingint returns the closest integer as the answer
![alt](images/12-numbers/2023-06-27-2g.png)

#### Creating Dates
- new Date constructor function pulls the current date and time and time zone
- passing in even part of a date to the date constructor function, it can parse the info and and return the entire d ate, time, and time zone
- this method is not the best practice though, because it can be unreliable
![alt](images/12-numbers/2023-06-27-3a.png)
- "Z" at end of date/time string is UTC- coordinated universal time (time without daylight savings)
![alt](images/12-numbers/2023-06-27-3b.png)
- passing in numbers to date constructor, js will parse the info into a new date string with date and time- months are based on 0 as jan, so 12 for month rolls into jan for the next year, a day number higher than the month has will roll forward too
![alt](images/12-numbers/2023-06-27-3c.png)
-single number passed into the date constructor function is the number of milliseconds since the beginning of unix time (Jan 1, 1970)
- to get the timestamp, multiply days, hours, minutes, seconds, milliseconds to add time to that in millisconds(ex is 3 days later)
- note to self: my computer displays 5 hours before that date/time because my computer is set to EST
![alt](images/12-numbers/2023-06-27-3d.png)
- Date object has its own methods, just like arrays, maps, strings, etc
- use getFullYear for 4 digit year (use this instead of getYear)
- getMonth is zero-based
- getDate returns the day number
- getDay returns the day of the week (zero based from Sunday)
- getHours, getMinutes, getSeconds, returns time
- getTime returns timestamp (time elapsed since Jan 1, 1970)
![alt](images/12-numbers/2023-06-27-3e.png)
- toISOString method returns a date/time string with Z ending for UTC time zone
![alt](images/12-numbers/2023-06-27-3f.png)
- Date.now() method returns the current moment's timestamp (time elapsed since Jan 1, 1970)
![alt](images/12-numbers/2023-06-27-3g.png)
- for all date/ time methods, use "set" instead of "get" to establish different date/time characteristics (ex: setFullYear)
![alt](images/12-numbers/2023-06-27-3h.png)

- to loop over 2 arrays at once, call forEach method on one of the arrays, then use the current index to loop through the second inside the same loop
![alt](images/12-numbers/2023-06-27-4.png)

### 6/29/23
- for more complex date/time calculations, use a js library (like moment js)

#### Internationalization
- To use the internationalization api, pass locale string into DateTimeFormat function of new Intl (internationalization api namespace)
- Locale string is the language and country (separated by a dash), ex "en-US" for English-USA
![alt](images/12-numbers/2023-06-29-1.png)
- list of locale strings: [W3 Schools Locale Strings](https://www.w3schools.com/jsref/jsref_tolocalestring.asp)
- call format method on the Intl namespace DateTimeFormat and pass in the date that you want it to format
![alt](images/12-numbers/2023-06-29-2.png)
- DateTimeFormat can take a second parameter that sets display options. Best to store these separately in an object variable to avoid cluttering the DateTimeFormat function call
![alt](images/12-numbers/2023-06-29-3.png)
- set the locale automatically with navigator language property, which pulls from user's browser
![alt](images/12-numbers/2023-06-29-4.png)
- non-date numbers can also be internationalized using Intl namespace, and number formater
- option number formatting options can also be applied: [number formatting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat)
- style can be either unit, percent, or currency
- if style is unit, specify what type of unit separately: [list of units](https://tc39.es/ecma402/#table-sanctioned-single-unit-identifiers)
- if style is currency, no unit is needed, but must define the currency (is NOT automatically determined by the locale), and can also optionally add a currencyDisplay
![alt](images/12-numbers/2023-06-29-5.png)

### 6/30/23

#### Timers
- setTimeout timer runs once, while setInterval runs indefinitely until stopped

#### setTimeout
- first parameter of setTimeout is the callback function- what it should do after the timeout
- second parameter is the time in milliseconds of the delay
- the timeout continues running in background, while the appropriate amount of time elapses, executing other code in the meantime- this is an example of asynchronous js
![alt](images/12-numbers/2023-06-30-1.png)
- arguments passed after the delay info are arguments for the function that is being delayed, and the input for the setTimeout function is the parameter name for those arguments
![alt](images/12-numbers/2023-06-30-2.png)
- to store the arguments in a separate array, pass them to the function with the spread operator, which essentially pulls them out of the array individually as function arguments
![alt](images/12-numbers/2023-06-30-3.png)

#### clearTimeout
- delayed function execution can be canceled during the time before the full timeout has passed using clearTimeout()
- clearTimeout takes the function name that is to be canceled, so timeout must be assigned to a name first
![alt](images/12-numbers/2023-06-30-4.png)

#### setInterval
- runs code on repeat at specified intervals until stopped
- first input is callback function (what to do after specified time)
- second input is time interval between function executions
![alt](images/12-numbers/2023-06-30-5.png)
- the function in setInterval does not execute immediately, but after the first interval of time, and then repeatedly at that interval until stopped, but the intial state is that it is not executed immediately
the workaround for this is to export it to a separate function that calls it immediately
![alt](images/12-numbers/2023-06-30-6.png)

#### clearInterval
- like clearTimeout, stops running the function at repeated intervals after a specified amount of time has elapsed
- input is name of function to stop executing
![alt](images/12-numbers/2023-06-30-7.png)


