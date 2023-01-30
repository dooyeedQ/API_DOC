
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
    Example of multiple-choice qestion:
    * Sentence： Virchow was the first scientist to discover that leukiemia is caused by rapid production of abnormal white blood cells.
    * Question：What is leukemia caused by?
    * Answer: rapid production of abnormal white blood cells
    * Distractors: 
      1. rapid reorganization of healthy white blood cells
      2. rapid expansion of immature neurons
      3. rapid production of useless tissues
              
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
    
    Example of cloze:
    * Sentence： Virchow was the first scientist to discover that leukiemia is caused by rapid production of abnormal white blood cells.
    * Question：Virchow was the first scientist to discover that leukiemia is caused by rapid production of ______.
    * Answer: abnormal white blood cells
    * Distractors: 
      1. healthy white blood cells
      2. immature neurons 
      3. useless tissues
     
                    
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
    
     Example of five of seven:
    * context：
The first microscopes powerful enough to distinguish blood cells were invented in the 1600s. By the early 1800s, scientists were able to distinguish white          blood cells from red blood cells. However, they didn't yet understand white blood cells' role in the immune system, helping to fight infection and other diseases. For that matter, they didn't understand there was such a thing as the immune system. Instead, they thought that these strange cells might be mucous or pus.In the 1840s and 1850s, several doctors wrote case studies of people who had swollen abdomens, fevers, weight loss, and weakness — symptoms that we now associate with leukemia. While performing blood tests during autopsies, the doctors noticed that these people had abnormal amounts of white blood cells — so much so that they described the disease as "white blood" or "leukemia." The name "leukemia" was derived from the Greek words "leukos," which means "white," and "haima," which means "blood." Doctors debated the cause of this abnormal level of white blood cells. In 1856, Rudolf Virchow, a German physician and pioneer in cellular pathology, proposed that the cause of leukemia would be found in the organs that produced the white blood cells — especially the spleen. Other doctors found that people with leukemia had bone marrow that was yellowish-green, instead of the normal, healthy red. Leukemia wasn't just a disease of the organs: The bones were involved as well. This destruction of the bone marrow accounted for the anemia (lack of red blood cells) that went along with leukemia.

    * Question：
The first microscopes powerful enough to distinguish blood cells were invented in the 1600s. _____ 1 _____ However, they didn't yet understand white blood cells' role in the immune system, helping to fight infection and other diseases.  _____ 2 _____  Instead, they thought that these strange cells might be muc
or pus. _____ 3 _____ While performing blood tests during autopsies, the doctors noticed that these people had abnormal amounts of white blood cells — so much so that they described the disease as "white blood" or "leukemia." The name "leukemia" was derived from the Greek words "leukos," which means "white," and "haima," which means "blood."  _____ 4 _____ In 1856, Rudolf Virchow, a German physician and pioneer in cellular pathology, proposed that the cause of leukemia would be found in the organs that produced the white blood cells — especially the spleen. Other doctors found that people with leukemia had bone marrow that was yellowish-green, instead of the normal, healthy red. _____ 5 _____ This destruction of the bone marrow accounted for the anemia (lack of red blood cells) that went along with leukemia
    * Answers:
      - 1. By the early 1800s, scientists were able to distinguish white blood cells from red blood cells.
      - 2. For that matter, they didn't understand there was such a thing as the immune system.
      - 3. In the 1840s and 1850s, several doctors wrote case studies of people who had swollen abdomens, fevers, weight loss, and weakness — symptoms that we now associate with leukemia.
      - 4. Doctors debated the cause of this abnormal level of white blood cells.
      - 5. Leukemia wasn't just a disease of the organs: The bones were involved as well.
    * Distractors: 
      - When a man's blood clot forms, it goes into the lungs.
      - Leukemia wasn't just a disease of the organs: The bones were involved as well.
    
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
    Example of fill in the blank:
    * Sentence： Virchow was the first scientist to discover that leukiemia is caused by rapid production of abnormal white blood cells.
    * Question：Virchow was the first scientist to discover that leukiemia is _____(cause) by rapid production of abnormal white blood cells.
    * Answer: caused
   
   
