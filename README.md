RELAX JSON
==========

A JSON schema language for humans.


Introduction
------------

Inspired by [RELAX NG Compact Syntax](http://www.relaxng.org/compact-tutorial-20030326.html) and [JSON](http://json.org) itself. 
RELAX JSON compares to [JSON Schema](http://json-schema.org/examples.html) as RELAX NG Compact compares to XML Schema.

One main reason why RELAX JSON being human-friendly is that it, itself, is not JSON. 
It is an entirely new language.


A contrived example
-------------------

The following is a pretty ridiculous example of what RELAX JSON looks like.
Readers familiar with JSON, RELAX NG or Regexes should recognize a few things here and there.

    BookLists [
      BookList+
      Store*
    ]
    
    BookList {
      books: [ Book* ]  
      owner: String 
    }
    
    Book {
      title:    String
      subtitle: String? 
      author:   String 
      ISBN:     String 
      weight:   Number 
      type:     BookType 
    }
    
    Store {
      name: String, url: String 
    }
    
    enum BookType {
      "Paperback",
      "Hardcover"
    }

This schema is valid for a JSON document such as:

    [
      {
        "books": [
          {
            "title": "Mijn leuk wereldje",
            "author": "Richard Scarry",
            "ISBN: "978-9024380329",
            "weight": 112,
            "type": "Paperback"
          },
          {
            "title": "Principia Discordia",
            "subtitle": "Or, How I Found Goddess and What I Did to Her When I Found Her: The Magnum Opiate of Malaclypse the Younger"
            "author": "Malaclypse the Younger",
            "ISBN: "978-1559500401",
            "weight": 130.4,
            "type": "Hardcover"
          },
        ],
        "owner": "George Clooney"
      },
      {
        "books": [],
        "owner": "George Bush"
      },
      {
        "name": "Amazon"
        "url": "http://www.amazon.com"
      },
      {
        "name": "Lulu"
        "url": "http://www.lulu.com"
      }
    ]


This example illustrates some notable language features:

* Types precede object key names
* Commas or newlines separate object elements
* Arrays can have mixed types. 
  In the example, `BookLists` is an array that mixes two types: `BookList` and `Store`.
* Array element counts can be specified with `+` and `*`. 
  In the example, `BookLists` must contain at least one `BookList`, and zero or more `Store`s.
* Optional fields are marked with a `?`. In the example, `subtitle` is an optional field. 
  All fields not marked optional are required.
* String fields that can only have one of a set of values can be specified by means of an `enum` type, 
  such as `BookType` in the example.