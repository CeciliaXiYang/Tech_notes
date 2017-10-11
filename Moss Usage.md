Reference: http://lightonphiri.org/blog/student-programming-plagiarism-dectection-using-moss  
Homepage: https://theory.stanford.edu/~aiken/moss/

-- Description: 
   MOSS(Measure of Software Similarity)
   Submission process: 
    1) Payload is checked and uploaded to the central server
    2) Once all files uploaded, a session query is submitted
    3) Central server returns the results in form of URL string: http://moss.stanford.edu/results/XXXXXXXX

-- Procedures: 
1 Registration:
  send an email to moss@moss.stanford.edu, with the exact content of: 
  registeruser 
  mail username@domain

2 Receive an email with the perl script
  Create a file named as moss.pl with the script

3 Payload cleaning:
  #!/usr/bin/bash
  # clean up resource folks
  for tmp in `find . -iname "__MACOSX"`; do echo "Removing... "$tmp; done
  for tmp in `find . -iname "__MACOSX"`; do rm -rf $tmp; done
  # move source code to root directories
  IFS=$'\n'
  for student in `ls`
    do for files in $student/*
       do if [ -d "$files" ]
             then for subfiles in `find "$files"`
                  do if [ -f $subfiles ]
                        then mv "$subfiles" $student/
                     fi
                  done
                  rm -rf $files
           fi
       done
     done
  
  ** _MACOSX files: the result of Apple storing Resource Forks safe manner
  
4 Submission script:
  usage: moss [-x] [-l language] [-d] [-b basefile1] ... [-b basefilen] [-m #] [-c "string"] file1 file2 file3
  
  -b Used to specify reference/base source code file
  -c Used to specify a comment string when submitting request
  -d Used to tell Moss that source code being compared is in directories
  -x Enables you to use experimental server in preference to production server
  -l Used to specify the programming language used in the source code to be processed
  -m Specifies maximum number of occurances of code before Moss ingores it—the default is 10
  -n Used to specify the total number of file recordsets to show on results page—the default is 250
  
  E.g perl moss.pl -l python -d */*py
  
5 Access the results URL: http://moss.stanford.edu/results/XXXXXXXX
  
