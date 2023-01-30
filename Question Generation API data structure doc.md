
# Post data structure:


```javascript
data={
      'key': a str if timestamp of this post request, 
      'text':content_html_text_data,
      'question_type': a_list_of_string_type_of_user_chooesed_question_type }
```
# Returned data structure:


```javascript
result={
      'key': a str if timestamp of this post request, 
      'data': a list of questions, each element is a dict, each type of question's structrue is expained below
      }
```
# API url:
http://wangserver.ddns.net:7233/api/question-generation
# All question types
```javascript-
['multiple-choice','cloze'，'cloze-five-of-seven'，'fill-in-the-blank']

```
# Returned data structure: 
* All the questions returend from question API will be in a list.  Each question data is a dict.


    # multiple-choice(Select one): 
           {"type": "multiple-choice",
            "question":[{"question": "What's the right answer?",
                        "answer": "this is right answer",
                        "options": ["option one.",  "option two.", "option three."]}]           }
              
    # cloze: 
            {"type": "cloze",
             "question":[{"answer":"this is right answer",
                          "options":["option one", "option two", "option three"],
                          "question_id": "0"},
                        
                         {"answer":"this is right answer",
                          "options":["option one", "option two", "option three"],
                          "question_id": "1"},
                          
 	                     {"answer":"this is right answer",
                          "options":["option one", "option two", "option three"],
                          "question_id": "2"}],
             "html":"
                    <p>
                        <span>
                            Church-key
                            <span question_id="0"></span>
                            pitchfork knausgaard, meh fashion 
                            <span question_id="1"></span>
                            kale chips organic meditation enamel pin tilde kogi.
                        </span>
                        <span>
                            Paleo forage yr glossier pug
                            <span question_id="1"></span>
                            photo booth locavore waistcoat 8-bit roof party activated charcoal.
                        </span>
                    </p>
                    <p>
                        <span>
                            Truffaut DIY
                            <span question_id="2"></span>
                            charcoal enamel pin freegan hella flexitarian knausgaard pug.
                        </span>
                    </p>"
            }
    
    # Example of cloze question generation:
    * sent data to api
      ```javascript
      data={
            'key': any timestamp string, 
            'text':"<p>Virchow was the first scientist to discover that leukiemia is caused by rapid production of abnormal white blood cells.</p>",
            'question_type': ['cloze'] }
      ```
    * result:
          {"type": "cloze",
             "question":[{"answer":"abnormal white blood cells",
                          "options":["healthy white blood cells", "immature neurons", "useless tissues"],
                          "question_id": "0"}
                          ],
             "html": "<p>
                        Virchow was the first scientist to discover that leukiemia is caused by rapid production of <span question_id="0">abnormal white blood cells</span>.
                     </p>"
            }
    
    

# Returned data structure:


```javascript
result={
      'key': a timestamp string, 
      'data': a list of questions, each element is a dict.
      }
```

# Data structure of cloze question

      {"type": "cloze",
       "question":[{"answer":"abnormal white blood cells",
                    "options":["healthy white blood cells", "immature neurons", "useless tissues"],
                    "question_id": "0"}
                    ],
       "html": "<p>
                  Virchow was the first scientist to discover that leukiemia is caused by rapid production of <span question_id="0">abnormal white blood cells</span>.
               </p>"
      }
                    
    # five of seven(choose 5)
           {"type": "cloze-five-of-seven",
            "question": { "answer":["0","3","5","7","9"],
                           "options":["this is option one", "this is option two"]
                           },
                           
                           
            "html": "
                    <p>
                        <span sent_id="0">
                            Church-key pitchfork knausgaard.
                        </span>
                        <span sent_id="1">
                            meh fashion kale chips organic meditation enamel pin tilde kogi.
                        </span>
                        <span sent_id="2">
                            Paleo forage yr glossier pug  photo booth locavore waistcoat 8-bit roof.
                        </span>
                    </p>
                    <p>
                        <span sent_id="3">
                            Truffaut DIY harcoal enamel pin freegan hella flexitarian.
                        </span>
                        <span sent_id="4">
                            charcoal enamel pin freegan hella flexitarian knausgaard pug.
                        </span>
                        <span sent_id="5">
                            hoodie iceland asymmetrical gastropub.
                        </span>
                        <span sent_id="6">
                            Normcore mustache trust fund kale chips.
                        </span>
                        <span sent_id="7">
                            meh fashion kale chips organic meditation enamel pin tilde kogi.
                        </span>
                    </p>
                    <p>
                        <span sent_id="8">
                            meh fashion kale chips organic meditation enamel pin tilde kogi.
                        </span>
                        <span sent_id="9">
                            Paleo forage yr glossier pug  photo booth locavore waistcoat 8-bit roof.
                        </span>
                    </p>"
            }
    
    # fill_in_blank
           {"type": "fill-in-the-blank",
            "question": [{"answer": "goes",
                         
                          "question_id": "0"},
                          
                         {"answer": "good",
                        
                          "question_id": "1"},
                          
                         {"answer": "left",

                          "question_id": "2"}],
            "html": "
                    <p>
                        <span >
                            Church-key
                            <span question_id="0"></span>
                            pitchfork knausgaard, meh fashion
                            <span question_id="1"></span>
                            kale chips organic meditation enamel pin tilde kogi.
                        </span>
                        <span >
                            Paleo forage yr glossier pug
                            <span question_id="1"></span>
                            photo booth locavore waistcoat 8-bit roof party activated charcoal.
                        </span>
                    </p>
                    <p>
                        <span>
                            Truffaut DIY
                            <span question_id="2"></span>
                            charcoal enamel pin freegan iceland asymmetrical gastropub.
                        </span>
                    </p>"
            }
            
    URL: http://wangserver.ddns.net:8633/api/question-generation

# Example post request:


```javascript
data={
      'key': any timestamp string, 
      'text':"<p>Virchow was the first scientist to discover that leukiemia is caused by rapid production of abnormal white blood cells.</p>",
      'question_type': ['cloze'] }
Each sentence used for generate cloze question should be labled with "<p></p>" tag
```

# Returned data structure:


```javascript
result={
      'key': a timestamp string, 
      'data': a list of questions, each element is a dict.
      }
```

# Data structure of cloze question

      {"type": "cloze",
       "question":[{"answer":"abnormal white blood cells",
                    "options":["healthy white blood cells", "immature neurons", "useless tissues"],
                    "question_id": "0"}
                    ],
       "html": "<p>
                  Virchow was the first scientist to discover that leukiemia is caused by rapid production of <span question_id="0">abnormal white blood cells</span>.
               </p>"
      }
