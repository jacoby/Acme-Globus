# NAME

    Globus - Object-Oriented interface to Globus

# DESCRIPTION

    Globus is a tool that allows the sharing of scientific data between 
    researchers and institutions. Globus enables you to transfer your 
    data using just a web browser, or using their SSH interface at 
    cli.globusonline.org.

    This is a client library for the Globus CLI.

    For detailed documentation of the API, 
    see http://dev.globus.org/cli/reference.

# CAVEATS

    This code is a work in progress, focusing on my needs at the moment 
    rather than covering all the capabilities of the Globus CLI. It is
    therefore very stubtastic.

    This module also relies very much on SSH, and thus the rules of 
    private and public keys. Therefore, using it as a shared tool would
    be ill-advised if not impossible.

# SYNOPSIS

    my $g = Globus->new($username,$path_to_ssh_key) ;
    $g->endpoint_add_shared( 'institution#endpoint', $directory, $endpoint_name ) ;
    $g->acl_add( $endpoint . '/', 'djacoby@example.com' ) ;
    

# METHODS

## BASICS

### **new**

    Creates a new Globus object. Takes two options: 
    the username and path to the SSH key you use to connect to Globus.

### **set\_username**

### **set\_key\_path**

### **get\_username**

### **get\_key\_path**

    These commands return and change the username and keypath you use to 
    connect to Globus.

## TASK MANAGEMENT

### **cancel**

### **details**

### **events**

### **modify**

### **status**

### **wait**

We do not do much with task management, so these are currently stubs.

## TASK CREATION

### **delete**

### **rm**

Currently stubs

### **scp**

### **transfer**

Both commands take a source, or from path (including endpoint),
a destination, or to path (includint endpoint), and a boolean indicating
whether you're copying recursively or not.

## FILE MANAGEMENT

### **ls**

Works?

### **rename**

### **mkdir**

Stubs

## ENDPOINT MANAGEMENT

### **acl\_add**

### **acl\_list**

### **acl\_remove**

acl-\* is the way that Globus refers to permissions

By the interface, Globus supports adding shares by email address, 
by Globus username or by Globus group name. This module sticks to
using email address. acl\_add() takes an endpoint, an email address 
you're sharing to, and a boolean indicating whether this share is
read-only or read-write. acl\_add() returns a share id.

acl\_remove() uses that share id to identify which shares are to be 
removed.

acl\_list() returns an array of hashes containing the information about 
each user with access to an endpoint, including the share ID and permissions.

### **endpoint\_add\_shared**

### **endpoint\_list**

### **endpoint\_search**

### **endpoint\_remove**

endpoint\_add\_shared() handles the specific case of creating an endpoint 
from an existing endpoint, not the general case.  It takes the endpoint
where you're sharing from, the path you're sharing, and the endpoint 
you're creating. If you are user 'user' and creating the endpoint 'test',
the command takes 'test', not 'user#test'.

endpoint\_remove and endpoint\_list, however, take a full endpoint name, like 'user#test'.

Current usage is endpoint\_list for a list of all our shares, and endpoint\_search
for details of each individual share

### **list\_my\_endpoints**

### **search\_my\_endpoints**

list\_my\_endpoints() and search\_my\_endpoints() were added once I discovered
the failings of existing list and search. These tools return a hashref
of hashrefs holding the owner, host\_endpoint, host\_endpoint\_name,
credential\_status, and most importantly, the id, legacy\_name and display\_name.

For older shares, legacy\_name will be something like 'purduegcore#hr00001\_firstshare'
and display\_name will be 'n/a', while for newer shares, legacy\_name will be
'purduegcore#SAME\_AS\_ID' and display\_name will be like older shares' legacy\_name,
'purduegcore#hr99999\_filled\_the\_space'. In both cases, the value you want
to use to get details or to remove a share is the id, which is a UUID. 

### **endpoint\_activate**

### **endpoint\_add**

### **endpoint\_deactivate**

### **endpoint\_modify**

### **endpoint\_rename**

Stubs

## OTHER

### **help**   

### **history**

### **man**         

### **profile**

### **versions**

profile() returns information about the Globus user, including the email address 
and public key.

Otherwise stubs

# LICENSE

Copyright (C) 2017, Dave Jacoby.

This program is free software, you can redistribute it and/or modify it 
under the terms of the Artistic License version 2.0.

# AUTHOR

Dave Jacoby - [jacoby.david@gmail.com](https://metacpan.org/pod/jacoby.david@gmail.com)
