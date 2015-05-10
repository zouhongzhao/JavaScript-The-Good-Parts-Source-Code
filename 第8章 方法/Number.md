chapter: Methods
==================
```javascript
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
    
```
