chapter: Methods
==================

var name = 'Curly';
var initial = name.charAt(0);    // initial is 'C'
    
    
====================================
String.method('charAt', function (pos) {
return this.slice(pos, pos + 1);
});
    
    
====================================
var name = 'Curly';
var initial = name.charCodeAt(0);    // initial is 67
    
    
====================================
var s = 'C'.concat('a', 't');    // s is 'Cat'
    
    
====================================
var text = 'Mississippi';
var p = text.indexOf('ss');    // p is 2
p = text.indexOf('ss', 3);     // p is 5
p = text.indexOf('ss', 6);     // p is -1
    
    
====================================
var text = 'Mississippi';
var p = text.lastIndexOf('ss');    // p is 5
p = text.lastIndexOf('ss', 3);     // p is 2
p = text.lastIndexOf('ss', 6);     // p is 5
    
    
====================================
var m = ['AAA', 'A', 'aa', 'a', 'Aa', 'aaa'];
m.sort(function (a, b) {
    return a.localeCompare(b);
});
// m (in some locale) is
//      ['a', 'A', 'aa', 'Aa', 'aaa', 'AAA']
    
    
====================================
var text = '<html><body bgcolor=linen><p>' +
        'This is <b>bold<\/b>!<\/p><\/body><\/html>';
var tags = /[^<>]+|<(\/?)([A-Za-z]+)([^<>]*)>/g;
var a, i;

a = text.match(tags);
for (i = 0; i < a.length; i += 1) {
    document.writeln(('// [' + i + '] ' + a[i]).entityify(  ));
}

// The result is

// [0] <html>
// [1] <body bgcolor=linen>
// [2] <p>
// [3] This is
// [4] <b>
// [5] bold
// [6] </b>
// [7] !
// [8] </p>
// [9] </body>
// [10] </html>
    
    
====================================
var result = "mother_in_law".replace('_', '-');
    
    
====================================
// Capture 3 digits within parens

var oldareacode = /\((\d{3})\)/g;
var p = '(555)666-1212'.replace(oldareacode, '$1-');
// p is '555-666-1212'
    
    
====================================
String.method('entityify', function (  ) {

    var character = {
        '<' : '&lt;',
        '>' : '&gt;',
        '&' : '&amp;',
        '"' : '&quot;'
    };

// Return the string.entityify method, which
// returns the result of calling the replace method.
// Its replaceValue function returns the result of
// looking a character up in an object. This use of
// an object usually outperforms switch statements.

    return function (  ) {
        return this.replace(/[<>&"]/g, function (c) {
            return character[c];
        });
    };
}(  ));
alert("<&>".entityify(  ));  // &lt;&amp;&gt;
    
    
====================================
var text = 'and in it he says "Any damn fool could';
var pos = text.search(/["']/);    // pos is 18
    
    
====================================
var text = 'and in it he says "Any damn fool could';
var a = text.slice(18);
// a is '"Any damn fool could'
var b = text.slice(0, 3);
// b is 'and'
var c = text.slice(-5);
// c is 'could'
var d = text.slice(19, 32);
// d is 'Any damn fool'
    
    
====================================
var digits = '0123456789';
var a = digits.split('', 5);
// a is ['0', '1', '2', '3', '4']
    
    
====================================
var ip = '192.168.1.0';
var b = ip.split('.');
// b is ['192', '168', '1', '0']

var c = '|a|b|c|'.split('|');
// c is ['', 'a', 'b', 'c', '']

var text = 'last,  first ,middle';
var d = text.split(/\s*,\s*/);
// d is [
//    'last',
//    'first',
//    'middle'
// ]
    
    
====================================
var e = text.split(/\s*(,)\s*/);
// e is [
//    'last',
//    ',',
//    'first',
//    ',',
//    'middle'
// ]
    
    
====================================
var f = '|a|b|c|'.split(/\|/);
// f is ['a', 'b', 'c'] on some systems, and
// f is ['', 'a', 'b', 'c', ''] on others
    
    
====================================
var a = String.fromCharCode(67, 97, 116);
// a is 'Cat'
    
    
==================