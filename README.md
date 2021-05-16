⦁	nav args sending a word from words fragment(list) to edit/add word fragment
⦁	we check the nullable option and set the default value to null therefore when we click the add button we dont need to send anything and it will send null so the apllications knows that we want to add a new item as it didnt recieve a word.
⦁	there are two places where we can get a handle to the arguments that we pass to the fragment which are the fragment itself and viewmodel but  as we know the viewmodel is the class responsible for providing the data that fragment has to present 
⦁	WE MADE A NEW VIEW MODEL
⦁	we can retrieve our navigations argument in the fragment and send them to view model but we also can reterieve them directly in the view model through the safe state handle 
⦁	target : today we want to delete all of the learned words so basicly after this we will know how to do something with a bunch of data with in a specific state another thing that we do is making a dialouge box as a new nav destination which makes it a seperate fragment with its own viewmodel and by doing this we made our alert dialouge totally reusable so if we needed it again somewhere else we will just navigate to the destination again and its done.
⦁	we need a new dao in order to delete words with the learned attribiute equal to true.
⦁	we made a query for this task and it looks like this

@Query("DELETE FROM word_table WHERE learned = 1")
suspend fun deleteLearnedWords()

⦁	now we should create the alert dialouge fragment and add it to the nav graph.
⦁	we dont need to make a layout for the dialouge we can just use the default layout and we only need to make the kotlin fragment class.
⦁	we make a  new package for this dialog fragment which has a kotlin class that inherits base dialog fragment
⦁	we add android entry point annotation because it uses its own view model
⦁	we override on create dialog it returns alertDIalog builder which needs context and as we are in the fragment we use requireContext() 
⦁	we set the title and the messege and we implement the cancel button and we call the viewmodel for the ok button here wo should call a function that calls the dao function for us
⦁	So we make the viewmodel and we inject viewmodel using dagger and also we add the dependencies that we need which are WordDao and applicationScope the annotation that we made before but why do we need it?
⦁	alright alright alert dialogs will dissmiss as soon as you click a button on them and its a default behaviour its not like we navigate back or something it just dissmisses and the point is when it happens the viewmodel will be removed from the memory together with fragment because its over. so the view model scope will be cancelled and it may be not enough for doing a dao operation and things get canceled in the middle of operation therefore we need a larger scope which would be the application scope that we just injected it wont be cancelled when the viewmodel is removed from the memory.
⦁	we connect the fragment to the viewModel and call the function that we made in the setPositiveButton click.
⦁	now we should add this fragment to our navigation graph
⦁	we added a global action to the dialog fragment and we go to the words fragment and call a new method in our viewmodel when the curresponding view is clicked.
⦁	In that method we send a new event in our word event channel in order to do this we have to make a new object in our sealed class 
⦁	now in the fragment in our events when statement we handle the new event and here we actually should navigate to the alert dialouge , we have to rebuild our project.
