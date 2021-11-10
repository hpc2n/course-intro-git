## Exercise

The purpose of this exercise is to learn about basic commands further.

1. Create a folder called "mysecondrepo" which will contain your repository. 
Tasks:
      - initialize the repository
      - create a README.md file and add this text on the first line: "File created on Sep. 30, 2020" 
      - stage the file
      - commit the changes
      - create a second file "Poem.md" without any text (hint: use touch command), stage and commit it
      
2. Copy and paste the two paragraphs below of the poem *la lluvia* by Jorge Luis Borges into the Poem.md file:
Tasks:
      - stage the first paragraph only
      - confirm that the file has been partially staged by checking the status. 
      - check if the staged changes correspond to just the first paragraph by looking at the differences between: 
      -- the working directory vs. the staging area 
      -- the staging area vs. the committed changes region (Repo) 
      - commit the staged changes and check the status
      - stage the second paragraph and commit the changes
      
<pre><code>
Bruscamente la tarde se ha aclarado
Porque ya cae la lluvia minuciosa.
Cae o cayó. La lluvia es una cosa
Que sin duda sucede en el pasado.

Quien la oye caer ha recobrado
El tiempo en que la suerte venturosa
Le reveló una flor llamada rosa
Y el curioso color del colorado.
</code></pre>      

3. Create a folder called "FirstPoem" and move the Poem.md file to this new folder (use git mv). 
Check the status to confirm that the file was moved. Commit the changes. 

4. (Challenge task) Add the next paragraph of the poem:

<pre><code>
Esta lluvia que ciega los cristales
Alegrará en perdidos arrabales
Las negras uvas de una parra en cierto

Patio que ya no existe. La mojada
Tarde me trae la voz, la voz deseada,
De mi padre que vuelve y que no ha muerto.
</code></pre>  

stage the changes and commit them. Now, we have the last four commits refering to the same topic (same poem). 
The goal of this part of the exercise is to summarize those four commits into a single one.

hint: git rebase -i HEAD~4

5. End of exercise
