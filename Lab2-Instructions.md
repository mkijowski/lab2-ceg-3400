## Lab 2 : CEG 3400

### Authentication and Permissions

Table of contents:
* [Background]()
* [Objectives]()
* [Preparation]()
* [Task 1: Account Setup]()
* [Task 2: Permissions Issues]()
* [Task 3: Advanced Permissions Issues]()

---

#### Background

Setting up accounts on a system can be a difficult task to do securely.  
In part one students will work in groups of 3 to setup multiple users on your 
VM.  Students will extract information from this virtual machine and document 
the process.

Parts 2 and 3 will involve checking and changing file permissions.

Part 4 will have students attempting to attack the weak passwords they 
created in part 1.

---

#### Objectives

Students should become familiar with the following:

* using encryption to secure communication within a team
* following instructions
* Standard authentication methods in linux
* File permissions in linux
* Special file permissions in linux
* cracking passwords

---

### Task 1 - Users

Intended to be done in a team of 2-3, but a single person *could* perform
all tasks.  ***All work should be done by each student***

* create a simple / insecure password you can share 
  (one or two words, not much L337 speak)
* create an SSH key pair
* deploy the AWS stack for this lab
* exchange passwords using gpg encryption (use the `--recipient` option)
* create ***an account for each team member*** using the above
* Back up the `/etc/shadow` file ***Submit this file to the pilot dropbox by next Thursday***

***Input needed in `README.md`***

---

### Task 2 - Permissions

It appears someone on your system *might* have used an insecure password.
Lets lock some things down.

* Check the permissions on each users home directory `~` (their username folder in `/home`)
* Change each users' home directory (and all contents of) permissions so only the file owner (`u`) and file group (`g`) can read/write/execute files.
* Check the permissions on `/etc/shadow`
* Using standard linux file permissions, allow ***just one*** of your group members read only access to your home directory.

---

### Task 3 - SetUID

The SetUID and SetGID bits can be tricky to think about.  Check out the 
`/code` provided to you in this lab.  Edit this as necessary to allow
***ANY*** user on this system to list contents of your home directory 
(using the executable generated by this code).

* Edit the code as necessary and compile
* Check ownership of this file
* Set the SetUID bit of this file
* Make sure others can read/execute this file
* Verify your teammates have successfully performed this task

---

### Task 4 - Hashcat

Crack those passwords!  More information will come next week with the 
condensed shadow file.

I have provided 3 wordlist files in `/wordlists`, you will need to extract
them as two are quite large (use `gunzip`).

You can try to figure out the graphical interface of hashcat or just run
it from the command line:

`hashcat-cli32.bin -m 1800 -a 0 -o hashcat.output --remove shadowfile wordlists/500_passwords.txt`

The above may run if everything I get you is named correctly...
* `-m 1800` is for cracking Unix type 6 hashed passwords (`$6` in the hash)
* `-a 0` specifies a dictionary attack
* output all foudn passwords to `hashcat.output`
* `--remove` removes cracked hashes from the shadowfile (so we dont waste time when using the next wordlists)
* get password hashes from `shadowfile`
* using the dictionary file `wordlists/500_passwords.txt`

[Samsclass]: https://samsclass.info/123/proj10/p12-hashcat.htm
