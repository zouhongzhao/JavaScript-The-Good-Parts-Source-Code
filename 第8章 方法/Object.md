chapter: Methods
==================

var a = {member: true};
var b = Object.create(a);              // from Chapter 3
var t = a.hasOwnProperty('member');   // t is true
var u = b.hasOwnProperty('member');   // u is false
var v = b.member;                     // v is true
    
    