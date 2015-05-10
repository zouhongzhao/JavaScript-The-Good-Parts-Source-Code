chapter: Methods
==================
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];
var c = a.concat(b, true);
// c is ['a', 'b', 'c', 'x', 'y', 'z', true]
    
    
====================================
var a = ['a', 'b', 'c'];
a.push('d');
var c = a.join('');    // c is 'abcd';
    
    
====================================
var a = ['a', 'b', 'c'];
var c = a.pop(  );    // a is ['a', 'b'] & c is 'c'
    
    
====================================
Array.method('pop', function (  ) {
    return this.splice(this.length - 1, 1)[0];
});
    
    
====================================
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];
var c = a.push(b, true);
// a is ['a', 'b', 'c', ['x', 'y', 'z'], true]
// c is 5;
    
    
====================================
Array.method('push', function (  ) {
    this.splice.apply(
        this,
        [this.length, 0].concat(Array.prototype.slice.apply(arguments)));
    return this.length;
});
    
    
====================================
var a = ['a', 'b', 'c'];
var b = a.reverse(  );
// both a and b are ['c', 'b', 'a']
    
    
====================================
var a = ['a', 'b', 'c'];
var c = a.shift(  );    // a is ['b', 'c'] & c is 'a'
    
    
====================================
Array.method('shift', function (  ) {
    return this.splice(0, 1)[0];
});
    
    
====================================
var a = ['a', 'b', 'c'];
var b = a.slice(0, 1);    // b is ['a']
var c = a.slice(1);       // c is ['b', 'c']
var d = a.slice(1, 2);    // d is ['b']
    
    
====================================
var n = [4, 8, 15, 16, 23, 42];
n.sort(  );
// n is [15, 16, 23, 4, 42, 8]
    
    
====================================
n.sort(function (a, b) {
    return a - b;
});
// n is [4, 8, 15, 16, 23, 42];
    
    
====================================
var m = ['aa', 'bb', 'a', 4, 8, 15, 16, 23, 42];
m.sort(function (a, b) {
    if (a === b) {
        return 0;
    }
    if (typeof a === typeof b) {
        return a < b ? -1 : 1;
    }
    return typeof a < typeof b ? -1 : 1;
});
// m is [4, 8, 15, 16, 23, 42, 'a', 'aa', 'bb']
    
    
====================================
// Function by takes a member name string and returns
// a comparison function that can be used to sort an
// array of objects that contain that member.

var by = function (name) {
    return function (o, p) {
        var a, b;
        if (typeof o === 'object' && typeof p === 'object' && o && p) {
            a = o[name];
            b = p[name];
            if (a === b) {
                return 0;
            }
            if (typeof a === typeof b) {
                return a < b ? -1 : 1;
            }
            return typeof a < typeof b ? -1 : 1;
        } else {
            throw {
                name: 'Error',
                message: 'Expected an object when sorting by ' + name;
            };
        }
    };
};

var s = [
    {first: 'Joe',   last: 'Besser'},
    {first: 'Moe',   last: 'Howard'},
    {first: 'Joe',   last: 'DeRita'},
    {first: 'Shemp', last: 'Howard'},
    {first: 'Larry', last: 'Fine'},
    {first: 'Curly', last: 'Howard'}
];
s.sort(by('first'));    // s is [
//    {first: 'Curly', last: 'Howard'},
//    {first: 'Joe',   last: 'DeRita'},
//    {first: 'Joe',   last: 'Besser'},
//    {first: 'Larry', last: 'Fine'},
//    {first: 'Moe',   last: 'Howard'},
//    {first: 'Shemp', last: 'Howard'}
// ]
    
    
====================================
s.sort(by('first')).sort(by('last'));
    
    
====================================
// Function by takes a member name string and an
// optional minor comparison function and returns
// a comparison function that can be used to sort an
// array of objects that contain that member. The
// minor comparison function is used to break ties
// when the o[name] and p[name] are equal.

var by = function (name, minor) {
    return function (o, p) {
        var a, b;
        if (o && p && typeof o === 'object' && typeof p === 'object') {
            a = o[name];
            b = p[name];
            if (a === b) {
                return typeof minor === 'function' ? minor(o, p) : 0;
            }
            if (typeof a === typeof b) {
                return a < b ? -1 : 1;
            }
            return typeof a < typeof b ? -1 : 1;
        } else {
            throw {
                name: 'Error',
                message: 'Expected an object when sorting by ' + name;
            };
        }
    };
};

s.sort(by('last', by('first')));    // s is [
//    {first: 'Joe',   last: 'Besser'},
//    {first: 'Joe',   last: 'DeRita'},
//    {first: 'Larry', last: 'Fine'},
//    {first: 'Curly', last: 'Howard'},
//    {first: 'Moe',   last: 'Howard'},
//    {first: 'Shemp', last: 'Howard'}
// ]
    
    
====================================
var a = ['a', 'b', 'c'];
var r = a.splice(1, 1, 'ache', 'bug');
// a is ['a', 'ache', 'bug', 'c']
// r is ['b']
    
    
====================================
Array.method('splice', function (start, deleteCount) {
    var max = Math.max,
        min = Math.min,
        delta,
        element,
        insertCount = max(arguments.length - 2, 0),
        k = 0,
        len = this.length,
        new_len,
        result = [],
        shift_count;

    start = start || 0;
    if (start < 0) {
        start += len;
    }
    start = max(min(start, len), 0);
    deleteCount = max(min(typeof deleteCount === 'number' ?
            deleteCount : len, len - start), 0);
    delta = insertCount - deleteCount;
    new_len = len + delta;
    while (k < deleteCount) {
        element = this[start + k];
        if (element !== undefined) {
            result[k] = element;
        }
        k += 1;
    }
    shift_count = len - start - deleteCount;
    if (delta < 0) {
        k = start + insertCount;
        while (shift_count) {
            this[k] = this[k - delta];
            k += 1;
            shift_count -= 1;
        }
        this.length = new_len;
    } else if (delta > 0) {
        k = 1;
        while (shift_count) {
            this[new_len - k] = this[len - k];
            k += 1;
            shift_count -= 1;
         }
            this.length = new_len;
     }
    for (k = 0; k < insertCount; k += 1) {
        this[start + k] = arguments[k + 2];
    }
    return result;
});
    
    
====================================
var a = ['a', 'b', 'c'];
var r = a.unshift('?', '@');
// a is ['?', '@', 'a', 'b', 'c']
// r is 5
    
    
====================================
Array.method('unshift', function (  ) {
    this.splice.apply(this,
        [0, 0].concat(Array.prototype.slice.apply(arguments)));
    return this.length;
});
    
    
====================================
Function.method('bind', function (that) {

// Return a function that will call this function as
// though it is a method of that object.

    var method = this,
        slice = Array.prototype.slice,
        args = slice.apply(arguments, [1]);
    return function (  ) {
        return method.apply(that,
            args.concat(slice.apply(arguments, [0])));
    };
});

var x = function (  ) {
    return this.value;
}.bind({value: 666});
alert(x(  )); // 666
    
    
====================================
document.writeln(Math.PI.toExponential(0));
document.writeln(Math.PI.toExponential(2));
document.writeln(Math.PI.toExponential(7));
document.writeln(Math.PI.toExponential(16));
document.writeln(Math.PI.toExponential(  ));

// Produces

3e+0
3.14e+0
3.1415927e+0
3.1415926535897930e+0
3.141592653589793e+0
    
    
====================================
document.writeln(Math.PI.toFixed(0));
document.writeln(Math.PI.toFixed(2));
document.writeln(Math.PI.toFixed(7));
document.writeln(Math.PI.toFixed(16));
document.writeln(Math.PI.toFixed(  ));

// Produces

3
3.14
3.1415927
3.1415926535897930
3
    
    
====================================
document.writeln(Math.PI.toPrecision(2));
document.writeln(Math.PI.toPrecision(7));
document.writeln(Math.PI.toPrecision(16));
document.writeln(Math.PI.toPrecision(  ));

// Produces

3.1
3.141593
3.141592653589793
3.141592653589793
    
    
====================================
document.writeln(Math.PI.toString(2));
document.writeln(Math.PI.toString(8));
document.writeln(Math.PI.toString(16));
document.writeln(Math.PI.toString(  ));

// Produces

11.001001000011111101101010100010001000010110100011
3.1103755242102643
3.243f6a8885a3
3.141592653589793
    
    
====================================
var a = {member: true};
var b = Object.create(a);              // from Chapter 3
var t = a.hasOwnProperty('member');   // t is true
var u = b.hasOwnProperty('member');   // u is false
var v = b.member;                     // v is true
    
    
====================================
// Break a simple html text into tags and texts.
// (See string.replace for the entityify method.)

// For each tag or text, produce an array containing
// [0] The full matched tag or text
// [1] The /, if there is one
// [2] The tag name
// [3] The attributes, if any

var text = '<html><body bgcolor=linen><p>' +
        'This is <b>bold<\/b>!<\/p><\/body><\/html>';
var tags = /[^<>]+|<(\/?)([A-Za-z]+)([^<>]*)>/g;
var a, i;

while ((a = tags.exec(text))) {
    for (i = 0; i < a.length; i += 1) {
        document.writeln(('// [' + i + '] ' + a[i]).entityify(  ));
    }
    document.writeln(  );
}

// Result:

// [0] <html>
// [1]
// [2] html
// [3]

// [0] <body bgcolor=linen>
// [1]
// [2] body
// [3]  bgcolor=linen

// [0] <p>
// [1]
// [2] p
// [3]

// [0] This is
// [1] undefined
// [2] undefined
// [3] undefined

// [0] <b>
// [1]
// [2] b
// [3]

// [0] bold
// [1] undefined
// [2] undefined
// [3] undefined

// [0] </b>
// [1] /
// [2] b
// [3]

// [0] !
// [1] undefined
// [2] undefined
// [3] undefined

// [0] </p>
// [1] /
// [2] p
// [3]

// [0] </body>
// [1] /
// [2] body
// [3]

// [0] </html>
// [1] /
// [2] html
// [3]
    
    
====================================
var b = /&.+;/.test('frank &amp; beans');
// b is true
    
    
====================================
RegExp.method('test', function (string) {
    return this.exec(string) !== null;
});
    
    
====================================
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