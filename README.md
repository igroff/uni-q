#### uni-q

##### What?

A simple system for enqueing unique operations for execution ( and executing them ). That is for a given operation that operation may only exist in the queue a single time.  So you can blindly schedule actions knowing that only a single instance will be executed, and no other instance of that action will be added to the queue until the enqueued instance is processed.

##### Definitions

* action - something placed in the queue for processing
* command - synonym for action
* queue entry - an executable file within the directory serving as the queue for uni-q. The intention is that these be shell scripts, but they can be any executable file.  The action will be unlinked on completion of processing.

##### Usage

    uni-q add [ command file ]

Actions can be provided to uni-q in couple ways: a path to a file provided on the command line, or via stdin.

If a file path is NOT specified on the command line invoking uni-q it will be assumed that commands are being provided on stdin.

The environment in which the command was added is preserved and used at command execution time.

Specifying a command file enqueues the execution of that file, thus if the file contents change between the time that it's execution is added to the queue and the actual execution of the command thew new file contents will be executed.

Return Codes
  * 0 - command enqueued successfully
  * 1 - invalid command file specified ( file does not exist )


    uni-q process

Processes all items in the queue in dictionary order of the command names. 

Return Codes
  * 0 - command(s) processed ( does not indicate outcome of command processing )
  * 1 - no commands processed ( queue is empty )
  *


##### Working Directory

uni-q manages it's queue and information about the execution of commands in its working directory which is, by default, ~/.uni-q . The structure is as follows.

~/.uni-q
    queue/
    command_logs/
    uni-q.log
    


