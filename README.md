# resumable-tasks
You have to do a task that is going to take long (like re-encoding A LOT of
videos, which was my inspiration for creating this program) but you want to
have the possibility to resume it later?

Just create a file like this (let's say its called todo.task)

	ffmpeg -i some_file1.mp4 <options> out_file1.mp4
	ffmpeg -i some_file2.mp4 <options> out_file2.mp4
	ffmpeg -i some_file3.mp4 <options> out_file3.mp4
	ffmpeg -i some_file4.mp4 <options> out_file4.mp4
	ffmpeg -i some_file5.mp4 <options> out_file5.mp4
	ffmpeg -i some_file6.mp4 <options> out_file6.mp4
	ffmpeg -i some_file7.mp4 <options> out_file7.mp4

and execute `resumable_task todo.task`

## How does it work

Usage: `./resumable_task <task file>`

The program will read the lines from top to bottom.
Each line shall be executed within a Bash subshell; this means you can use all
the Bash substitutions, line continuations and such. If the exit status of the
line executed is 0, remove the current line and go on until the file is empty.
If the exit status is not 0 then abort the execution with a error message.
