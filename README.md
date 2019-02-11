# Intro

The goal is to create user friendly asserteable classes to be used in python tests from a schema file, with the
main goal of extendability of the schema type (Swagger, Avro and etc).

## Flow Design

Basic flow of the generation:

* Parsing the schema to general structure with a given parser per message in the schema, a parsing plan, which will contain all the relevant information from the schema (will be described later on). The parser API should be general and not bound to any Avro specification, so different sources parsers could be implemented. 
* Base on the parsing plan and the python generator, which will contain the different templates for all use cases (class generation, adding import statements adn etc).

## Implementation

### Parsing Plan

The plan will contain the following:

* Needed imports which will contain:
  * Basic imports (will be supplied to the python generator).
  * Accumulated imports requirements.
* Schema name (will be the package name, which will contain this schema generation output).
* Message name (which will be the class name).
* Message attributes list, which each attribute will contain:
  * Attribute name.
  * Attribute Python type as string.
  * Path in the message.
  * Is required flag.

### Parser

inputs:

* Mapping between schema types to python imports with a relevant default value.
* Basic imports list, will be needed to prevent unnecessary imports.

### Generated Code

* Python package with the schema name.
* Each message will be located in it's own module.
* While each module will contain:
  * Imports list (with basic imports and message specific imports dependencies).
  * Class with the message name inheriting from the basic classes (TODO: Not sure if needed or what is the best why to supply this).
  * The class will contain the relevant attributes 
