⦁	nav args sending a word from words fragment(list) to edit/add word fragment
⦁	we check the nullable option and set the default value to null therefore when we click the add button we dont need to send anything and it will send null so the apllications knows that we want to add a new item as it didnt recieve a word.
⦁	there are two places where we can get a handle to the arguments that we pass to the fragment which are the fragment itself and viewmodel but  as we know the viewmodel is the class responsible for providing the data that fragment has to present 
⦁	WE MADE A NEW VIEW MODEL
⦁	we can retrieve our navigations argument in the fragment and send them to view model but we also can reterieve them directly in the view model through the safe state handle 
⦁	
