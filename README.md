# ReaderAbilityChecker
"""ReaderAbilityChecker computes the grade level for text stored in a text file.
The input to this program is the name of a text file. The outputs are the number
of words, and the reader ability grade of the reader.  """


import os
dire=os.getcwd()
listOfdir=os.listdir(dire)
while True:
    
    UserFileName=raw_input("Enter file name:")
    if (UserFileName in listOfdir) and    (UserFileName.endswith('.txt')):
        InputFile=open(UserFileName,'r')
        text=InputFile.read()

        sentence=text.count(".") + text.count('!') + \
                  text.count(";") + text.count(":") + \
                  text.count("?")

        words=len(text.split())
        syllable=0

        for word in text.split():
            for vowel in ['a','e','i','o','u']:
                syllable += word.count(vowel)
            for ending in ['es','ed','e']:
                if word.endswith(ending):
                    syllable -= 1
            if word.endswith('le'):
                    syllable += 1
        
        if words!=0 and sentence != 0 and syllable != 0:
            G=round((0.39*words)/sentence+ (11.8*syllable)/words-15.59)
            if G >= 0 and G <=30:
                print 'The Readability level is College'
            elif  G >= 50 and G <=60:
                print 'The Readability level is High School'
            elif  G >= 90 and G <=100:
                print 'The Readability level is fourth grade'
                     
        print 'This text has %d words' %(words)
        
    elif UserFileName not in listOfdir:
        print "This text file does not exist in current directory"
    elif not(UserFileName.endswith('.txt')):
             print "This is not a text file."



