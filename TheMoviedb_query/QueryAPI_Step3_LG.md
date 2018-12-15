

```python
import requests
import json
from pprint import pprint
import pandas as pd
import time
```


```python
moviecsv_data = 'TheSilverScreenProject/DataCleaning/Wholelist_NameColumn'

list_df = pd.read_csv(moviecsv_data)
list_df.head(5)
#purchase_df.count()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Award</th>
      <th>Winner</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Actor in a Leading Role</td>
      <td>1.0</td>
      <td>Philip Seymour Hoffman</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Actor in a Leading Role</td>
      <td>NaN</td>
      <td>Terrence Howard</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Actor in a Leading Role</td>
      <td>NaN</td>
      <td>Heath Ledger</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Actor in a Leading Role</td>
      <td>NaN</td>
      <td>Joaquin Phoenix</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Actor in a Leading Role</td>
      <td>NaN</td>
      <td>David Strathairn</td>
    </tr>
  </tbody>
</table>
</div>




```python
dflist = list_df['Name'].tolist()
print(dflist)
```

    ['Philip Seymour Hoffman', 'Terrence Howard', 'Heath Ledger', 'Joaquin Phoenix', 'David Strathairn', 'George Clooney', 'Matt Dillon', 'Paul Giamatti', 'Jake Gyllenhaal', 'William Hurt', 'Judi Dench', 'Felicity Huffman', 'Keira Knightley', 'Charlize Theron', 'Reese Witherspoon', 'Amy Adams', 'Catherine Keener', 'Frances McDormand', 'Rachel Weisz', 'Michelle Williams', "Howl's Moving Castle ", "Tim Burton's Corpse Bride ", 'Wallace & Gromit in The Curse of the Were-Rabbit ', 'Good Night, and Good Luck. ', 'Harry Potter and the Goblet of Fire ', 'King Kong ', 'Memoirs of a Geisha ', 'Pride & Prejudice ', 'Batman Begins ', 'Brokeback Mountain ', 'Good Night, and Good Luck. ', 'Memoirs of a Geisha ', 'The New World ', 'Charlie and the Chocolate Factory ', 'Memoirs of a Geisha ', 'Mrs. Henderson Presents ', 'Pride & Prejudice ', 'Walk the Line ', 'Brokeback Mountain ', 'Capote ', 'Crash ', 'Good Night, and Good Luck. ', 'Munich ', "Darwin's Nightmare ", 'Enron: The Smartest Guys in the Room ', 'March of the Penguins ', 'Murderball ', 'Street Fight ', 'The Death of Kevin Carter: Casualty of the Bang Bang Club ', 'God Sleeps in Rwanda ', 'The Mushroom Club ', 'A Note of Triumph: The Golden Age of Norman Corwin ', 'Cinderella Man ', 'The Constant Gardener ', 'Crash ', 'Munich ', 'Walk the Line ', "Don't Tell ", 'Joyeux Noël ', 'Paradise Now ', 'Sophie Scholl - The Final Days ', 'Tsotsi ', 'The Chronicles of Narnia: The Lion, the Witch and the Wardrobe ', 'Cinderella Man ', 'Star Wars: Episode III Revenge of the Sith ', 'Brokeback Mountain ', 'The Constant Gardener ', 'Memoirs of a Geisha ', 'Munich ', 'Pride & Prejudice ', '"In The Deep" from Crash', '"It\'s Hard Out Here For A Pimp" from Hustle & Flow', '"Travelin\' Thru" from Transamerica', 'Brokeback Mountain ', 'Capote ', 'Crash ', 'Good Night, and Good Luck. ', 'Munich ', 'Badgered ', 'The Moon and the Son: An Imagined Conversation ', 'The Mysterious Geographic Explorations of Jasper Morello ', '9', 'One Man Band ', 'Ausreisser (The Runaway) ', 'Cashback ', 'The Last Farm ', 'Our Time Is Up ', 'Six Shooter ', 'King Kong ', 'Memoirs of a Geisha ', 'War of the Worlds ', 'The Chronicles of Narnia: The Lion, the Witch and the Wardrobe ', 'King Kong ', 'Memoirs of a Geisha ', 'Walk the Line ', 'War of the Worlds ', 'The Chronicles of Narnia: The Lion, the Witch and the Wardrobe ', 'King Kong ', 'War of the Worlds ', 'Brokeback Mountain ', 'Capote ', 'The Constant Gardener ', 'A History of Violence ', 'Munich ', 'Crash ', 'Good Night, and Good Luck. ', 'Match Point ', 'The Squid and the Whale ', 'Syriana ', 'Robert Altman', 'Gary Demos', 'Don Hall', 'Leonardo DiCaprio', 'Ryan Gosling', "Peter O'Toole", 'Will Smith', 'Forest Whitaker', 'Alan Arkin', 'Jackie Earle Haley', 'Djimon Hounsou', 'Eddie Murphy', 'Mark Wahlberg', 'Penélope Cruz', 'Judi Dench', 'Helen Mirren', 'Meryl Streep', 'Kate Winslet', 'Adriana Barraza', 'Cate Blanchett', 'Abigail Breslin', 'Jennifer Hudson', 'Rinko Kikuchi', 'Cars ', 'Happy Feet ', 'Monster House ', 'Dreamgirls ', 'The Good Shepherd ', "Pan's Labyrinth ", "Pirates of the Caribbean: Dead Man's Chest ", 'The Prestige ', 'The Black Dahlia ', 'Children of Men ', 'The Illusionist ', "Pan's Labyrinth ", 'The Prestige ', 'Curse of the Golden Flower ', 'The Devil Wears Prada ', 'Dreamgirls ', 'Marie Antoinette ', 'The Queen ', 'Babel ', 'The Departed ', 'Letters from Iwo Jima ', 'The Queen ', 'United 93 ', 'Deliver Us from Evil ', 'An Inconvenient Truth ', 'Iraq in Fragments ', 'Jesus Camp ', 'My Country, My Country ', 'The Blood of Yingzhou District ', 'Recycled Life ', 'Rehearsing a Dream ', 'Two Hands ', 'Babel ', 'Blood Diamond ', 'Children of Men ', 'The Departed ', 'United 93 ', 'After the Wedding ', 'Days of Glory (Indigènes) ', 'The Lives of Others ', "Pan's Labyrinth ", 'Water ', 'Apocalypto ', 'Click ', "Pan's Labyrinth ", 'Babel ', 'The Good German ', 'Notes on a Scandal ', "Pan's Labyrinth ", 'The Queen ', '"I Need To Wake Up" from An Inconvenient Truth', '"Listen" from Dreamgirls', '"Love You I Do" from Dreamgirls', '"Our Town" from Cars', '"Patience" from Dreamgirls', 'Babel ', 'The Departed ', 'Letters from Iwo Jima ', 'Little Miss Sunshine ', 'The Queen ', 'The Danish Poet ', 'Lifted ', 'The Little Matchgirl ', 'Maestro ', 'No Time for Nuts ', 'Binta and the Great Idea (Binta Y La Gran Idea) ', 'Éramos Pocos (One Too Many) ', 'Helmer & Son ', 'The Saviour ', 'West Bank Story ', 'Apocalypto ', 'Blood Diamond ', 'Flags of Our Fathers ', 'Letters from Iwo Jima ', "Pirates of the Caribbean: Dead Man's Chest ", 'Apocalypto ', 'Blood Diamond ', 'Dreamgirls ', 'Flags of Our Fathers ', "Pirates of the Caribbean: Dead Man's Chest ", "Pirates of the Caribbean: Dead Man's Chest ", 'Poseidon ', 'Superman Returns ', 'Borat Cultural Learnings of America for Make Benefit Glorious Nation of Kazakhstan ', 'Children of Men ', 'The Departed ', 'Little Children ', 'Notes on a Scandal ', 'Babel ', 'Letters from Iwo Jima ', 'Little Miss Sunshine ', "Pan's Labyrinth ", 'The Queen ', 'Sherry Lansing', 'Ennio Morricone', 'Ray Feeney', 'Ioan Allen, J. Wayne Anderson, Mary Ann Anderson, Ted Costas, Paul R. Goldberg, Shawn Jones, Thomas Kuhn, Dr. Alan Masson, Colin Mossman, Martin Richards, Frank Ricotta and Richard C. Sehlin', 'Richard Edlund', 'George Clooney', 'Daniel Day-Lewis', 'Johnny Depp', 'Tommy Lee Jones', 'Viggo Mortensen', 'Casey Affleck', 'Javier Bardem', 'Philip Seymour Hoffman', 'Hal Holbrook', 'Tom Wilkinson', 'Cate Blanchett', 'Julie Christie', 'Marion Cotillard', 'Laura Linney', 'Ellen Page', 'Cate Blanchett', 'Ruby Dee', 'Saoirse Ronan', 'Amy Ryan', 'Tilda Swinton', 'Persepolis ', 'Ratatouille ', "Surf's Up ", 'American Gangster ', 'Atonement ', 'The Golden Compass ', 'Sweeney Todd The Demon Barber of Fleet Street ', 'There Will Be Blood ', 'The Assassination of Jesse James by the Coward Robert Ford ', 'Atonement ', 'The Diving Bell and the Butterfly ', 'No Country for Old Men ', 'There Will Be Blood ', 'Across the Universe ', 'Atonement ', 'Elizabeth: The Golden Age ', 'La Vie en Rose ', 'Sweeney Todd The Demon Barber of Fleet Street ', 'The Diving Bell and the Butterfly ', 'Juno ', 'Michael Clayton ', 'No Country for Old Men ', 'There Will Be Blood ', 'No End in Sight ', 'Operation Homecoming: Writing the Wartime Experience ', 'Sicko ', 'Taxi to the Dark Side ', 'War/Dance ', 'Freeheld ', 'La Corona (The Crown) ', 'Salim Baba ', "Sari's Mother ", 'The Bourne Ultimatum ', 'The Diving Bell and the Butterfly ', 'Into the Wild ', 'No Country for Old Men ', 'There Will Be Blood ', 'Beaufort ', 'The Counterfeiters ', 'Katyn ', 'Mongol ', '12', 'La Vie en Rose ', 'Norbit ', "Pirates of the Caribbean: At World's End ", 'Atonement ', 'The Kite Runner ', 'Michael Clayton ', 'Ratatouille ', '3:10 to Yuma ', '"Falling Slowly" from Once', '"Happy Working Song" from Enchanted', '"Raise It Up" from August Rush', '"So Close" from Enchanted', '"That\'s How You Know" from Enchanted', 'Atonement ', 'Juno ', 'Michael Clayton ', 'No Country for Old Men ', 'There Will Be Blood ', 'I Met the Walrus ', 'Madame Tutli-Putli ', 'Même les Pigeons Vont au Paradis (Even Pigeons Go to Heaven) ', 'My Love (Moya Lyubov) ', 'Peter & the Wolf ', 'At Night ', 'Il Supplente (The Substitute) ', 'Le Mozart des Pickpockets (The Mozart of Pickpockets) ', 'Tanghi Argentini ', 'The Tonto Woman ', 'The Bourne Ultimatum ', 'No Country for Old Men ', 'Ratatouille ', 'There Will Be Blood ', 'Transformers ', 'The Bourne Ultimatum ', 'No Country for Old Men ', 'Ratatouille ', '3:10 to Yuma ', 'Transformers ', 'The Golden Compass ', "Pirates of the Caribbean: At World's End ", 'Transformers ', 'Atonement ', 'Away from Her ', 'The Diving Bell and the Butterfly ', 'No Country for Old Men ', 'There Will Be Blood ', 'Juno ', 'Lars and the Real Girl ', 'Michael Clayton ', 'Ratatouille ', 'The Savages ', 'Robert Boyle', 'David A. Grafton', 'Jonathan Erland', 'David Inglish', 'Richard Jenkins', 'Frank Langella', 'Sean Penn', 'Brad Pitt', 'Mickey Rourke', 'Josh Brolin', 'Robert Downey Jr.', 'Philip Seymour Hoffman', 'Heath Ledger', 'Michael Shannon', 'Anne Hathaway', 'Angelina Jolie', 'Melissa Leo', 'Meryl Streep', 'Kate Winslet', 'Amy Adams', 'Penélope Cruz', 'Viola Davis', 'Taraji P. Henson', 'Marisa Tomei', 'Bolt ', 'Kung Fu Panda ', 'WALL-E ', 'Changeling ', 'The Curious Case of Benjamin Button ', 'The Dark Knight ', 'The Duchess ', 'Revolutionary Road ', 'Changeling ', 'The Curious Case of Benjamin Button ', 'The Dark Knight ', 'The Reader ', 'Slumdog Millionaire ', 'Australia ', 'The Curious Case of Benjamin Button ', 'The Duchess ', 'Milk ', 'Revolutionary Road ', 'The Curious Case of Benjamin Button ', 'Frost/Nixon ', 'Milk ', 'The Reader ', 'Slumdog Millionaire ', 'The Betrayal (Nerakhoon) ', 'Encounters at the End of the World ', 'The Garden ', 'Man on Wire ', 'Trouble the Water ', 'The Conscience of Nhem En ', 'The Final Inch ', 'Smile Pinki ', 'The Witness - From the Balcony of Room 306 ', 'The Curious Case of Benjamin Button ', 'The Dark Knight ', 'Frost/Nixon ', 'Milk ', 'Slumdog Millionaire ', 'The Baader Meinhof Complex ', 'The Class ', 'Departures ', 'Revanche ', 'Waltz with Bashir ', 'The Curious Case of Benjamin Button ', 'The Dark Knight ', 'Hellboy II: The Golden Army ', 'The Curious Case of Benjamin Button ', 'Defiance ', 'Milk ', 'Slumdog Millionaire ', 'WALL-E ', '"Down To Earth" from WALL-E', '"Jai Ho" from Slumdog Millionaire', '"O Saya" from Slumdog Millionaire', 'The Curious Case of Benjamin Button ', 'Frost/Nixon ', 'Milk ', 'The Reader ', 'Slumdog Millionaire ', 'La Maison en Petits Cubes ', 'Lavatory - Lovestory ', 'Oktapodi ', 'Presto ', 'This Way Up ', 'Auf der Strecke (On the Line) ', 'Manon on the Asphalt ', 'New Boy ', 'The Pig ', 'Spielzeugland (Toyland) ', 'The Dark Knight ', 'Iron Man ', 'Slumdog Millionaire ', 'WALL-E ', 'Wanted ', 'The Curious Case of Benjamin Button ', 'The Dark Knight ', 'Slumdog Millionaire ', 'WALL-E ', 'Wanted ', 'The Curious Case of Benjamin Button ', 'The Dark Knight ', 'Iron Man ', 'The Curious Case of Benjamin Button ', 'Doubt ', 'Frost/Nixon ', 'The Reader ', 'Slumdog Millionaire ', 'Frozen River ', 'Happy-Go-Lucky ', 'In Bruges ', 'Milk ', 'WALL-E ', 'Jerry Lewis', 'Ed Catmull', 'Mark Kimball', 'Jeff Bridges', 'George Clooney', 'Colin Firth', 'Morgan Freeman', 'Jeremy Renner', 'Matt Damon', 'Woody Harrelson', 'Christopher Plummer', 'Stanley Tucci', 'Christoph Waltz', 'Sandra Bullock', 'Helen Mirren', 'Carey Mulligan', 'Gabourey Sidibe', 'Meryl Streep', 'Penélope Cruz', 'Vera Farmiga', 'Maggie Gyllenhaal', 'Anna Kendrick', "Mo'Nique", 'Coraline ', 'Fantastic Mr. Fox ', 'The Princess and the Frog ', 'The Secret of Kells ', 'Up ', 'Avatar ', 'The Imaginarium of Doctor Parnassus ', 'Nine ', 'Sherlock Holmes ', 'The Young Victoria ', 'Avatar ', 'Harry Potter and the Half-Blood Prince ', 'The Hurt Locker ', 'Inglourious Basterds ', 'The White Ribbon ', 'Bright Star ', 'Coco before Chanel ', 'The Imaginarium of Doctor Parnassus ', 'Nine ', 'The Young Victoria ', 'Avatar ', 'The Hurt Locker ', 'Inglourious Basterds ', "Precious: Based on the Novel 'Push' by Sapphire ", 'Up in the Air ', 'Burma VJ ', 'The Cove ', 'Food, Inc. ', 'The Most Dangerous Man in America: Daniel Ellsberg and the Pentagon Papers ', 'Which Way Home ', "China's Unnatural Disaster: The Tears of Sichuan Province ", 'The Last Campaign of Governor Booth Gardner ', 'The Last Truck: Closing of a GM Plant ', 'Music by Prudence ', 'Rabbit à la Berlin ', 'Avatar ', 'District 9 ', 'The Hurt Locker ', 'Inglourious Basterds ', "Precious: Based on the Novel 'Push' by Sapphire ", 'Ajami ', 'The Milk of Sorrow ', 'A Prophet ', 'The Secret in Their Eyes ', 'The White Ribbon ', 'Il Divo ', 'Star Trek ', 'The Young Victoria ', 'Avatar ', 'Fantastic Mr. Fox ', 'The Hurt Locker ', 'Sherlock Holmes ', 'Up ', '"Almost There" from The Princess and the Frog', '"Down In New Orleans" from The Princess and the Frog', '"Loin De Paname" from Paris 36', '"Take It All" from Nine', '"The Weary Kind (Theme From Crazy Heart)" from Crazy Heart', 'Avatar ', 'The Blind Side ', 'District 9 ', 'An Education ', 'The Hurt Locker ', 'Inglourious Basterds ', "Precious: Based on the Novel 'Push' by Sapphire ", 'A Serious Man ', 'Up ', 'Up in the Air ', 'French Roast ', "Granny O'Grimm's Sleeping Beauty ", 'The Lady and the Reaper (La Dama y la Muerte) ', 'Logorama ', 'A Matter of Loaf and Death ', 'The Door ', 'Instead of Abracadabra ', 'Kavi ', 'Miracle Fish ', 'The New Tenants ', 'Avatar ', 'The Hurt Locker ', 'Inglourious Basterds ', 'Star Trek ', 'Up ', 'Avatar ', 'The Hurt Locker ', 'Inglourious Basterds ', 'Star Trek ', 'Transformers: Revenge of the Fallen ', 'Avatar ', 'District 9 ', 'Star Trek ', 'District 9 ', 'An Education ', 'In the Loop ', "Precious: Based on the Novel 'Push' by Sapphire ", 'Up in the Air ', 'The Hurt Locker ', 'Inglourious Basterds ', 'The Messenger ', 'A Serious Man ', 'Up ', 'Lauren Bacall', 'Roger Corman', 'Gordon Willis', 'John Calley', 'Javier Bardem', 'Jeff Bridges', 'Jesse Eisenberg', 'Colin Firth', 'James Franco', 'Christian Bale', 'John Hawkes', 'Jeremy Renner', 'Mark Ruffalo', 'Geoffrey Rush', 'Annette Bening', 'Nicole Kidman', 'Jennifer Lawrence', 'Natalie Portman', 'Michelle Williams', 'Amy Adams', 'Helena Bonham Carter', 'Melissa Leo', 'Hailee Steinfeld', 'Jacki Weaver', 'How to Train Your Dragon ', 'The Illusionist ', 'Toy Story 3 ', 'Alice in Wonderland ', 'Harry Potter and the Deathly Hallows Part 1 ', 'Inception ', "The King's Speech ", 'True Grit ', 'Black Swan ', 'Inception ', "The King's Speech ", 'The Social Network ', 'True Grit ', 'Alice in Wonderland ', 'I Am Love ', "The King's Speech ", 'The Tempest ', 'True Grit ', 'Black Swan ', 'The Fighter ', "The King's Speech ", 'The Social Network ', 'True Grit ', 'Exit through the Gift Shop ', 'Gasland ', 'Inside Job ', 'Restrepo ', 'Waste Land ', 'Killing in the Name ', 'Poster Girl ', 'Strangers No More ', 'Sun Come Up ', 'The Warriors of Qiugang ', 'Black Swan ', 'The Fighter ', "The King's Speech ", '127 Hours ', 'The Social Network ', 'Biutiful ', 'Dogtooth ', 'In a Better World ', 'Incendies ', 'Outside the Law (Hors-la-loi) ', "Barney's Version ", 'The Way Back ', 'The Wolfman ', 'How to Train Your Dragon ', 'Inception ', "The King's Speech ", '127 Hours ', 'The Social Network ', '"Coming Home" from Country Strong', '"I See The Light" from Tangled', '"If I Rise" from 127 Hours', '"We Belong Together" from Toy Story 3', 'Black Swan ', 'The Fighter ', 'Inception ', 'The Kids Are All Right ', "The King's Speech ", '127 Hours ', 'The Social Network ', 'Toy Story 3 ', 'True Grit ', "Winter's Bone ", 'Day & Night ', 'The Gruffalo ', "Let's Pollute ", 'The Lost Thing ', 'Madagascar, carnet de voyage (Madagascar, a Journey Diary) ', 'The Confession ', 'The Crush ', 'God of Love ', 'Na Wewe ', 'Wish 143 ', 'Inception ', 'Toy Story 3 ', 'Tron: Legacy ', 'True Grit ', 'Unstoppable ', 'Inception ', "The King's Speech ", 'Salt ', 'The Social Network ', 'True Grit ', 'Alice in Wonderland ', 'Harry Potter and the Deathly Hallows Part 1 ', 'Hereafter ', 'Inception ', 'Iron Man 2 ', '127 Hours ', 'The Social Network ', 'Toy Story 3 ', 'True Grit ', "Winter's Bone ", 'Another Year ', 'The Fighter ', 'Inception ', 'The Kids Are All Right ', "The King's Speech ", 'Kevin Brownlow', 'Jean-Luc Godard', 'Eli Wallach', 'Francis Ford Coppola', 'Denny Clairmont', 'Demián Bichir', 'George Clooney', 'Jean Dujardin', 'Gary Oldman', 'Brad Pitt', 'Kenneth Branagh', 'Jonah Hill', 'Nick Nolte', 'Christopher Plummer', 'Max von Sydow', 'Glenn Close', 'Viola Davis', 'Rooney Mara', 'Meryl Streep', 'Michelle Williams', 'Bérénice Bejo', 'Jessica Chastain', 'Melissa McCarthy', 'Janet McTeer', 'Octavia Spencer', 'A Cat in Paris ', 'Chico & Rita ', 'Kung Fu Panda 2 ', 'Puss in Boots ', 'Rango ', 'The Artist ', 'Harry Potter and the Deathly Hallows Part 2 ', 'Hugo ', 'Midnight in Paris ', 'War Horse ', 'The Artist ', 'The Girl with the Dragon Tattoo ', 'Hugo ', 'The Tree of Life ', 'War Horse ', 'Anonymous ', 'The Artist ', 'Hugo ', 'Jane Eyre ', 'W.E. ', 'The Artist ', 'The Descendants ', 'Hugo ', 'Midnight in Paris ', 'The Tree of Life ', 'Hell and Back Again ', 'If a Tree Falls: A Story of the Earth Liberation Front ', 'Paradise Lost 3: Purgatory ', 'Pina ', 'Undefeated ', 'The Barber of Birmingham: Foot Soldier of the Civil Rights Movement ', 'God Is the Bigger Elvis ', 'Incident in New Baghdad ', 'Saving Face ', 'The Tsunami and the Cherry Blossom ', 'The Artist ', 'The Descendants ', 'The Girl with the Dragon Tattoo ', 'Hugo ', 'Moneyball ', 'Bullhead ', 'Footnote ', 'In Darkness ', 'Monsieur Lazhar ', 'A Separation ', 'Albert Nobbs ', 'Harry Potter and the Deathly Hallows Part 2 ', 'The Iron Lady ', 'The Adventures of Tintin ', 'The Artist ', 'Hugo ', 'Tinker Tailor Soldier Spy ', 'War Horse ', '"Man Or Muppet" from The Muppets', '"Real In Rio" from Rio', 'The Artist ', 'The Descendants ', 'Extremely Loud & Incredibly Close ', 'The Help ', 'Hugo ', 'Midnight in Paris ', 'Moneyball ', 'The Tree of Life ', 'War Horse ', 'Dimanche/Sunday ', 'The Fantastic Flying Books of Mr. Morris Lessmore ', 'La Luna ', 'A Morning Stroll ', 'Wild Life ', 'Pentecost ', 'Raju ', 'The Shore ', 'Time Freak ', 'Tuba Atlantic ', 'Drive ', 'The Girl with the Dragon Tattoo ', 'Hugo ', 'Transformers: Dark of the Moon ', 'War Horse ', 'The Girl with the Dragon Tattoo ', 'Hugo ', 'Moneyball ', 'Transformers: Dark of the Moon ', 'War Horse ', 'Harry Potter and the Deathly Hallows Part 2 ', 'Hugo ', 'Real Steel ', 'Rise of the Planet of the Apes ', 'Transformers: Dark of the Moon ', 'The Descendants ', 'Hugo ', 'The Ides of March ', 'Moneyball ', 'Tinker Tailor Soldier Spy ', 'The Artist ', 'Bridesmaids ', 'Margin Call ', 'Midnight in Paris ', 'A Separation ', 'Oprah Winfrey', 'James Earl Jones.', 'Dick Smith', 'Douglas Trumbull', 'Jonathan Erland', 'Bradley Cooper', 'Daniel Day-Lewis', 'Hugh Jackman', 'Joaquin Phoenix', 'Denzel Washington', 'Alan Arkin', 'Robert De Niro', 'Philip Seymour Hoffman', 'Tommy Lee Jones', 'Christoph Waltz', 'Jessica Chastain', 'Jennifer Lawrence', 'Emmanuelle Riva', 'Quvenzhané Wallis', 'Naomi Watts', 'Amy Adams', 'Sally Field', 'Anne Hathaway', 'Helen Hunt', 'Jacki Weaver', 'Brave ', 'Frankenweenie ', 'ParaNorman ', 'The Pirates! Band of Misfits ', 'Wreck-It Ralph ', 'Anna Karenina ', 'Django Unchained ', 'Life of Pi ', 'Lincoln ', 'Skyfall ', 'Anna Karenina ', 'Les Misérables ', 'Lincoln ', 'Mirror Mirror ', 'Snow White and the Huntsman ', 'Amour ', 'Beasts of the Southern Wild ', 'Life of Pi ', 'Lincoln ', 'Silver Linings Playbook ', '5 Broken Cameras ', 'The Gatekeepers ', 'How to Survive a Plague ', 'The Invisible War ', 'Searching for Sugar Man ', 'Inocente ', 'Kings Point ', 'Mondays at Racine ', 'Open Heart ', 'Redemption ', 'Argo ', 'Life of Pi ', 'Lincoln ', 'Silver Linings Playbook ', 'Zero Dark Thirty ', 'Amour ', 'Kon-Tiki ', 'No ', 'A Royal Affair ', 'War Witch ', 'Hitchcock ', 'The Hobbit: An Unexpected Journey ', 'Les Misérables ', 'Anna Karenina ', 'Argo ', 'Life of Pi ', 'Lincoln ', 'Skyfall ', '"Before My Time" from Chasing Ice', '"Everybody Needs A Best Friend" from Ted', '"Pi\'s Lullaby" from Life of Pi', '"Skyfall" from Skyfall', '"Suddenly" from Les Misérables', 'Amour ', 'Argo ', 'Beasts of the Southern Wild ', 'Django Unchained ', 'Les Misérables ', 'Life of Pi ', 'Lincoln ', 'Silver Linings Playbook ', 'Zero Dark Thirty ', 'Anna Karenina ', 'The Hobbit: An Unexpected Journey ', 'Les Misérables ', 'Life of Pi ', 'Lincoln ', 'Adam and Dog ', 'Fresh Guacamole ', 'Head over Heels ', 'Maggie Simpson in "The Longest Daycare" ', 'Paperman ', 'Asad ', 'Buzkashi Boys ', 'Curfew ', 'Death of a Shadow (Dood van een Schaduw) ', 'Henry ', 'Argo ', 'Django Unchained ', 'Life of Pi ', 'Skyfall ', 'Zero Dark Thirty ', 'Argo ', 'Les Misérables ', 'Life of Pi ', 'Lincoln ', 'Skyfall ', 'The Hobbit: An Unexpected Journey ', 'Life of Pi ', "Marvel's The Avengers ", 'Prometheus ', 'Snow White and the Huntsman ', 'Argo ', 'Beasts of the Southern Wild ', 'Life of Pi ', 'Lincoln ', 'Silver Linings Playbook ', 'Amour ', 'Django Unchained ', 'Flight ', 'Moonrise Kingdom ', 'Zero Dark Thirty ', 'Jeffrey Katzenberg', 'Hal Needham', 'D.A. Pennebaker', 'George Stevens, Jr.', 'Bill Taylor', 'Christian Bale', 'Bruce Dern', 'Leonardo DiCaprio', 'Chiwetel Ejiofor', 'Matthew McConaughey', 'Barkhad Abdi', 'Bradley Cooper', 'Michael Fassbender', 'Jonah Hill', 'Jared Leto', 'Amy Adams', 'Cate Blanchett', 'Sandra Bullock', 'Judi Dench', 'Meryl Streep', 'Sally Hawkins', 'Jennifer Lawrence', "Lupita Nyong'o", 'Julia Roberts', 'June Squibb', 'The Croods ', 'Despicable Me 2 ', 'Ernest & Celestine ', 'Frozen ', 'The Wind Rises ', 'The Grandmaster ', 'Gravity ', 'Inside Llewyn Davis ', 'Nebraska ', 'Prisoners ', 'American Hustle ', 'The Grandmaster ', 'The Great Gatsby ', 'The Invisible Woman ', '12 Years a Slave ', 'American Hustle ', 'Gravity ', 'Nebraska ', '12 Years a Slave ', 'The Wolf of Wall Street ', 'The Act of Killing ', 'Cutie and the Boxer ', 'Dirty Wars ', 'The Square ', '20 Feet from Stardom ', 'CaveDigger ', 'Facing Fear ', 'Karama Has No Walls ', 'The Lady in Number 6: Music Saved My Life ', 'Prison Terminal: The Last Days of Private Jack Hall ', 'American Hustle ', 'Captain Phillips ', 'Dallas Buyers Club ', 'Gravity ', '12 Years a Slave ', 'The Broken Circle Breakdown ', 'The Great Beauty ', 'The Hunt ', 'The Missing Picture ', 'Omar ', 'Dallas Buyers Club ', 'Jackass Presents: Bad Grandpa ', 'The Lone Ranger ', 'The Book Thief ', 'Gravity ', 'Her ', 'Philomena ', 'Saving Mr. Banks ', '"Alone Yet Not Alone" from Alone Yet Not Alone', '"Happy" from Despicable Me 2', '"Let It Go" from Frozen', '"The Moon Song" from Her', '"Ordinary Love" from Mandela: Long Walk to Freedom', 'American Hustle ', 'Captain Phillips ', 'Dallas Buyers Club ', 'Gravity ', 'Her ', 'Nebraska ', 'Philomena ', '12 Years a Slave ', 'The Wolf of Wall Street ', 'American Hustle ', 'Gravity ', 'The Great Gatsby ', 'Her ', '12 Years a Slave ', 'Feral ', 'Get a Horse! ', 'Mr. Hublot ', 'Possessions ', 'Room on the Broom ', "Aquel No Era Yo (That Wasn't Me) ", 'Avant Que De Tout Perdre (Just before Losing Everything) ', 'Helium ', 'Pitääkö Mun Kaikki Hoitaa? (Do I Have to Take Care of Everything?) ', 'The Voorman Problem ', 'All Is Lost ', 'Captain Phillips ', 'Gravity ', 'The Hobbit: The Desolation of Smaug ', 'Lone Survivor ', 'Captain Phillips ', 'Gravity ', 'The Hobbit: The Desolation of Smaug ', 'Inside Llewyn Davis ', 'Lone Survivor ', 'Gravity ', 'The Hobbit: The Desolation of Smaug ', 'Iron Man 3 ', 'The Lone Ranger ', 'Star Trek Into Darkness ', 'Before Midnight ', 'Captain Phillips ', 'Philomena ', '12 Years a Slave ', 'The Wolf of Wall Street ', 'American Hustle ', 'Blue Jasmine ', 'Dallas Buyers Club ', 'Her ', 'Nebraska ', 'Angelina Jolie', 'Angela Lansbury', 'Steve Martin', 'Piero Tosi', 'Peter W. Anderson', 'Charles "Tad" Marburg', 'Steve Carell', 'Bradley Cooper', 'Benedict Cumberbatch', 'Michael Keaton', 'Eddie Redmayne', 'Robert Duvall', 'Ethan Hawke', 'Edward Norton', 'Mark Ruffalo', 'J.K. Simmons', 'Marion Cotillard', 'Felicity Jones', 'Julianne Moore', 'Rosamund Pike', 'Reese Witherspoon', 'Patricia Arquette', 'Laura Dern', 'Keira Knightley', 'Emma Stone', 'Meryl Streep', 'Big Hero 6 ', 'The Boxtrolls ', 'How to Train Your Dragon 2 ', 'Song of the Sea ', 'The Tale of the Princess Kaguya ', 'Birdman or (The Unexpected Virtue of Ignorance) ', 'The Grand Budapest Hotel ', 'Ida ', 'Mr. Turner ', 'Unbroken ', 'The Grand Budapest Hotel ', 'Inherent Vice ', 'Into the Woods ', 'Maleficent ', 'Mr. Turner ', 'Birdman or (The Unexpected Virtue of Ignorance) ', 'Boyhood ', 'Foxcatcher ', 'The Grand Budapest Hotel ', 'The Imitation Game ', 'CitizenFour ', 'Finding Vivian Maier ', 'Last Days in Vietnam ', 'The Salt of the Earth ', 'Virunga ', 'Crisis Hotline: Veterans Press 1 ', 'Joanna ', 'Our Curse ', 'The Reaper (La Parka) ', 'White Earth ', 'American Sniper ', 'Boyhood ', 'The Grand Budapest Hotel ', 'The Imitation Game ', 'Whiplash ', 'Ida ', 'Leviathan ', 'Tangerines ', 'Timbuktu ', 'Wild Tales ', 'Foxcatcher ', 'The Grand Budapest Hotel ', 'Guardians of the Galaxy ', 'The Grand Budapest Hotel ', 'The Imitation Game ', 'Interstellar ', 'Mr. Turner ', 'The Theory of Everything ', '"Everything Is Awesome" from The Lego Movie', '"Glory" from Selma', '"Grateful" from Beyond the Lights', '"I\'m Not Gonna Miss You" from Glen Campbell...I\'ll Be Me', '"Lost Stars" from Begin Again', 'American Sniper ', 'Birdman or (The Unexpected Virtue of Ignorance) ', 'Boyhood ', 'The Grand Budapest Hotel ', 'The Imitation Game ', 'Selma ', 'The Theory of Everything ', 'Whiplash ', 'The Grand Budapest Hotel ', 'The Imitation Game ', 'Interstellar ', 'Into the Woods ', 'Mr. Turner ', 'The Bigger Picture ', 'The Dam Keeper ', 'Feast ', 'Me and My Moulton ', 'A Single Life ', 'Aya ', 'Boogaloo and Graham ', 'Butter Lamp (La Lampe Au Beurre De Yak) ', 'Parvaneh ', 'The Phone Call ', 'American Sniper ', 'Birdman or (The Unexpected Virtue of Ignorance) ', 'The Hobbit: The Battle of the Five Armies ', 'Interstellar ', 'Unbroken ', 'American Sniper ', 'Birdman or (The Unexpected Virtue of Ignorance) ', 'Interstellar ', 'Unbroken ', 'Whiplash ', 'Captain America: The Winter Soldier ', 'Dawn of the Planet of the Apes ', 'Guardians of the Galaxy ', 'Interstellar ', 'X-Men: Days of Future Past ', 'American Sniper ', 'The Imitation Game ', 'Inherent Vice ', 'The Theory of Everything ', 'Whiplash ', 'Birdman or (The Unexpected Virtue of Ignorance) ', 'Boyhood ', 'Foxcatcher ', 'The Grand Budapest Hotel ', 'Nightcrawler ', 'Harry Belafonte', 'Jean-Claude Carrière', 'Hayao Miyazaki', "Maureen O'Hara", 'David Winchester Gray', 'Steven Tiffen, Jeff Cohen and Michael Fecik', 'Bryan Cranston', 'Matt Damon', 'Leonardo DiCaprio', 'Michael Fassbender', 'Eddie Redmayne', 'Christian Bale', 'Tom Hardy', 'Mark Ruffalo', 'Mark Rylance', 'Sylvester Stallone', 'Cate Blanchett', 'Brie Larson', 'Jennifer Lawrence', 'Charlotte Rampling', 'Saoirse Ronan', 'Jennifer Jason Leigh', 'Rooney Mara', 'Rachel McAdams', 'Alicia Vikander', 'Kate Winslet', 'Anomalisa', 'Boy and the World', 'Inside Out', 'Shaun the Sheep Movie', 'When Marnie Was There', 'Carol', 'The Hateful Eight', 'Mad Max: Fury Road', 'The Revenant', 'Sicario', 'Carol', 'Cinderella', 'The Danish Girl', 'Mad Max: Fury Road', 'The Revenant', 'The Big Short', 'Mad Max: Fury Road', 'The Revenant', 'Room', 'Spotlight', 'Amy', 'Cartel Land', 'The Look of Silence', 'What Happened, Miss Simone?', "Winter on Fire: Ukraine's Fight for Freedom", 'Body Team 12', 'Chau, Beyond the Lines', 'Claude Lanzmann: Spectres of the Shoah', 'A Girl in the River: The Price of Forgiveness', 'Last Day of Freedom', 'The Big Short', 'Mad Max: Fury Road', 'The Revenant', 'Spotlight', 'Star Wars: The Force Awakens', 'Embrace of the Serpent', 'Mustang', 'Son of Saul', 'Theeb', 'A War', 'Mad Max: Fury Road', 'The 100-Year-Old Man Who Climbed Out the Window and Disappeared', 'The Revenant', 'Bridge of Spies', 'Carol', 'The Hateful Eight', 'Sicario', 'Star Wars: The Force Awakens', '"Earned It" from Fifty Shades of Grey', 'Manta Ray from Racing Extinction', 'Simple Song #3 from Youth', '"Til It Happens To You" from The Hunting Ground', "Writing's On The Wall from Spectre", 'The Big Short', 'Bridge of Spies', 'Brooklyn', 'Mad Max: Fury Road', 'The Martian', 'The Revenant', 'Room', 'Spotlight', 'Bridge of Spies', 'The Danish Girl', 'Mad Max: Fury Road', 'The Martian', 'The Revenant', 'Bear Story', 'Prologue', "Sanjay's Super Team", "We Can't Live without Cosmos", 'World of Tomorrow', 'Ave Maria', 'Day One', 'Everything Will Be Okay (Alles Wird Gut)', 'Shok', 'Stutterer', 'Mad Max: Fury Road', 'The Martian', 'The Revenant', 'Sicario', 'Star Wars: The Force Awakens', 'Bridge of Spies', 'Mad Max: Fury Road', 'The Martian', 'The Revenant', 'Star Wars: The Force Awakens', 'Ex Machina', 'Mad Max: Fury Road', 'The Martian', 'The Revenant', 'Star Wars: The Force Awakens', 'The Big Short', 'Brooklyn', 'Carol', 'The Martian', 'Room', 'Bridge of Spies', 'Ex Machina', 'Inside Out', 'Spotlight', 'Straight Outta Compton', 'Debbie Reynolds', 'Spike Lee', 'Gena Rowlands']
    


```python
id_list = []
url = "https://api.themoviedb.org/3/search/movie?"
api_key = "api_key=98e159931ae83a9fde8ba0f8c795951d"
search_k = "&query="
```


```python
#response = requests.get(url + api_key + search_k + user_input)
#print(response.url)
call_count1 = 1
error_count = 0
sets1 = 1
```


```python
for movie in dflist:
    try:
        print(f'Processing Record {call_count1} of set{sets1} | {movie}')
        response = requests.get(url + api_key + search_k + movie)
        data = response.json()
        id_list.append((data['results'][0]['id']))
        print(response.url)  
    except Exception as e:
        print(type(e))
        print(str(e))
        error_count = error_count + 1
    call_count1 = call_count1 + 1
    if call_count1 == 241:
        call_count1 = 1
        sets1 = sets1 +1
        time.sleep(60)
print(f'------------------------------ \n End of Data Retrieval \n------------------------------')
print(error_count)
```

    Processing Record 1 of set1 | Philip Seymour Hoffman
    <class 'IndexError'>
    list index out of range
    Processing Record 2 of set1 | Terrence Howard
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Terrence%20Howard
    Processing Record 3 of set1 | Heath Ledger
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Heath%20Ledger
    Processing Record 4 of set1 | Joaquin Phoenix
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Joaquin%20Phoenix
    Processing Record 5 of set1 | David Strathairn
    <class 'IndexError'>
    list index out of range
    Processing Record 6 of set1 | George Clooney
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=George%20Clooney
    Processing Record 7 of set1 | Matt Dillon
    <class 'IndexError'>
    list index out of range
    Processing Record 8 of set1 | Paul Giamatti
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Paul%20Giamatti
    Processing Record 9 of set1 | Jake Gyllenhaal
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jake%20Gyllenhaal
    Processing Record 10 of set1 | William Hurt
    <class 'IndexError'>
    list index out of range
    Processing Record 11 of set1 | Judi Dench
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Judi%20Dench
    Processing Record 12 of set1 | Felicity Huffman
    <class 'IndexError'>
    list index out of range
    Processing Record 13 of set1 | Keira Knightley
    <class 'IndexError'>
    list index out of range
    Processing Record 14 of set1 | Charlize Theron
    <class 'IndexError'>
    list index out of range
    Processing Record 15 of set1 | Reese Witherspoon
    <class 'IndexError'>
    list index out of range
    Processing Record 16 of set1 | Amy Adams
    <class 'IndexError'>
    list index out of range
    Processing Record 17 of set1 | Catherine Keener
    <class 'IndexError'>
    list index out of range
    Processing Record 18 of set1 | Frances McDormand
    <class 'IndexError'>
    list index out of range
    Processing Record 19 of set1 | Rachel Weisz
    <class 'IndexError'>
    list index out of range
    Processing Record 20 of set1 | Michelle Williams
    <class 'IndexError'>
    list index out of range
    Processing Record 21 of set1 | Howl's Moving Castle 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Howl's%20Moving%20Castle%20
    Processing Record 22 of set1 | Tim Burton's Corpse Bride 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tim%20Burton's%20Corpse%20Bride%20
    Processing Record 23 of set1 | Wallace & Gromit in The Curse of the Were-Rabbit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Wallace%20&%20Gromit%20in%20The%20Curse%20of%20the%20Were-Rabbit%20
    Processing Record 24 of set1 | Good Night, and Good Luck. 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Good%20Night,%20and%20Good%20Luck.%20
    Processing Record 25 of set1 | Harry Potter and the Goblet of Fire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Potter%20and%20the%20Goblet%20of%20Fire%20
    Processing Record 26 of set1 | King Kong 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=King%20Kong%20
    Processing Record 27 of set1 | Memoirs of a Geisha 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Memoirs%20of%20a%20Geisha%20
    Processing Record 28 of set1 | Pride & Prejudice 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pride%20&%20Prejudice%20
    Processing Record 29 of set1 | Batman Begins 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Batman%20Begins%20
    Processing Record 30 of set1 | Brokeback Mountain 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brokeback%20Mountain%20
    Processing Record 31 of set1 | Good Night, and Good Luck. 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Good%20Night,%20and%20Good%20Luck.%20
    Processing Record 32 of set1 | Memoirs of a Geisha 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Memoirs%20of%20a%20Geisha%20
    Processing Record 33 of set1 | The New World 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20New%20World%20
    Processing Record 34 of set1 | Charlie and the Chocolate Factory 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Charlie%20and%20the%20Chocolate%20Factory%20
    Processing Record 35 of set1 | Memoirs of a Geisha 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Memoirs%20of%20a%20Geisha%20
    Processing Record 36 of set1 | Mrs. Henderson Presents 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mrs.%20Henderson%20Presents%20
    Processing Record 37 of set1 | Pride & Prejudice 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pride%20&%20Prejudice%20
    Processing Record 38 of set1 | Walk the Line 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Walk%20the%20Line%20
    Processing Record 39 of set1 | Brokeback Mountain 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brokeback%20Mountain%20
    Processing Record 40 of set1 | Capote 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Capote%20
    Processing Record 41 of set1 | Crash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Crash%20
    Processing Record 42 of set1 | Good Night, and Good Luck. 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Good%20Night,%20and%20Good%20Luck.%20
    Processing Record 43 of set1 | Munich 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Munich%20
    Processing Record 44 of set1 | Darwin's Nightmare 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Darwin's%20Nightmare%20
    Processing Record 45 of set1 | Enron: The Smartest Guys in the Room 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Enron:%20The%20Smartest%20Guys%20in%20the%20Room%20
    Processing Record 46 of set1 | March of the Penguins 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=March%20of%20the%20Penguins%20
    Processing Record 47 of set1 | Murderball 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Murderball%20
    Processing Record 48 of set1 | Street Fight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Street%20Fight%20
    Processing Record 49 of set1 | The Death of Kevin Carter: Casualty of the Bang Bang Club 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Death%20of%20Kevin%20Carter:%20Casualty%20of%20the%20Bang%20Bang%20Club%20
    Processing Record 50 of set1 | God Sleeps in Rwanda 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=God%20Sleeps%20in%20Rwanda%20
    Processing Record 51 of set1 | The Mushroom Club 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Mushroom%20Club%20
    Processing Record 52 of set1 | A Note of Triumph: The Golden Age of Norman Corwin 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Note%20of%20Triumph:%20The%20Golden%20Age%20of%20Norman%20Corwin%20
    Processing Record 53 of set1 | Cinderella Man 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Cinderella%20Man%20
    Processing Record 54 of set1 | The Constant Gardener 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Constant%20Gardener%20
    Processing Record 55 of set1 | Crash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Crash%20
    Processing Record 56 of set1 | Munich 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Munich%20
    Processing Record 57 of set1 | Walk the Line 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Walk%20the%20Line%20
    Processing Record 58 of set1 | Don't Tell 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Don't%20Tell%20
    Processing Record 59 of set1 | Joyeux Noël 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Joyeux%20No%C3%ABl%20
    Processing Record 60 of set1 | Paradise Now 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Paradise%20Now%20
    Processing Record 61 of set1 | Sophie Scholl - The Final Days 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sophie%20Scholl%20-%20The%20Final%20Days%20
    Processing Record 62 of set1 | Tsotsi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tsotsi%20
    Processing Record 63 of set1 | The Chronicles of Narnia: The Lion, the Witch and the Wardrobe 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Chronicles%20of%20Narnia:%20The%20Lion,%20the%20Witch%20and%20the%20Wardrobe%20
    Processing Record 64 of set1 | Cinderella Man 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Cinderella%20Man%20
    Processing Record 65 of set1 | Star Wars: Episode III Revenge of the Sith 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Wars:%20Episode%20III%20Revenge%20of%20the%20Sith%20
    Processing Record 66 of set1 | Brokeback Mountain 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brokeback%20Mountain%20
    Processing Record 67 of set1 | The Constant Gardener 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Constant%20Gardener%20
    Processing Record 68 of set1 | Memoirs of a Geisha 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Memoirs%20of%20a%20Geisha%20
    Processing Record 69 of set1 | Munich 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Munich%20
    Processing Record 70 of set1 | Pride & Prejudice 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pride%20&%20Prejudice%20
    Processing Record 71 of set1 | "In The Deep" from Crash
    <class 'IndexError'>
    list index out of range
    Processing Record 72 of set1 | "It's Hard Out Here For A Pimp" from Hustle & Flow
    <class 'IndexError'>
    list index out of range
    Processing Record 73 of set1 | "Travelin' Thru" from Transamerica
    <class 'IndexError'>
    list index out of range
    Processing Record 74 of set1 | Brokeback Mountain 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brokeback%20Mountain%20
    Processing Record 75 of set1 | Capote 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Capote%20
    Processing Record 76 of set1 | Crash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Crash%20
    Processing Record 77 of set1 | Good Night, and Good Luck. 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Good%20Night,%20and%20Good%20Luck.%20
    Processing Record 78 of set1 | Munich 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Munich%20
    Processing Record 79 of set1 | Badgered 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Badgered%20
    Processing Record 80 of set1 | The Moon and the Son: An Imagined Conversation 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Moon%20and%20the%20Son:%20An%20Imagined%20Conversation%20
    Processing Record 81 of set1 | The Mysterious Geographic Explorations of Jasper Morello 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Mysterious%20Geographic%20Explorations%20of%20Jasper%20Morello%20
    Processing Record 82 of set1 | 9
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=9
    Processing Record 83 of set1 | One Man Band 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=One%20Man%20Band%20
    Processing Record 84 of set1 | Ausreisser (The Runaway) 
    <class 'IndexError'>
    list index out of range
    Processing Record 85 of set1 | Cashback 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Cashback%20
    Processing Record 86 of set1 | The Last Farm 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Last%20Farm%20
    Processing Record 87 of set1 | Our Time Is Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Our%20Time%20Is%20Up%20
    Processing Record 88 of set1 | Six Shooter 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Six%20Shooter%20
    Processing Record 89 of set1 | King Kong 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=King%20Kong%20
    Processing Record 90 of set1 | Memoirs of a Geisha 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Memoirs%20of%20a%20Geisha%20
    Processing Record 91 of set1 | War of the Worlds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20of%20the%20Worlds%20
    Processing Record 92 of set1 | The Chronicles of Narnia: The Lion, the Witch and the Wardrobe 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Chronicles%20of%20Narnia:%20The%20Lion,%20the%20Witch%20and%20the%20Wardrobe%20
    Processing Record 93 of set1 | King Kong 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=King%20Kong%20
    Processing Record 94 of set1 | Memoirs of a Geisha 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Memoirs%20of%20a%20Geisha%20
    Processing Record 95 of set1 | Walk the Line 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Walk%20the%20Line%20
    Processing Record 96 of set1 | War of the Worlds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20of%20the%20Worlds%20
    Processing Record 97 of set1 | The Chronicles of Narnia: The Lion, the Witch and the Wardrobe 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Chronicles%20of%20Narnia:%20The%20Lion,%20the%20Witch%20and%20the%20Wardrobe%20
    Processing Record 98 of set1 | King Kong 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=King%20Kong%20
    Processing Record 99 of set1 | War of the Worlds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20of%20the%20Worlds%20
    Processing Record 100 of set1 | Brokeback Mountain 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brokeback%20Mountain%20
    Processing Record 101 of set1 | Capote 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Capote%20
    Processing Record 102 of set1 | The Constant Gardener 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Constant%20Gardener%20
    Processing Record 103 of set1 | A History of Violence 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20History%20of%20Violence%20
    Processing Record 104 of set1 | Munich 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Munich%20
    Processing Record 105 of set1 | Crash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Crash%20
    Processing Record 106 of set1 | Good Night, and Good Luck. 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Good%20Night,%20and%20Good%20Luck.%20
    Processing Record 107 of set1 | Match Point 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Match%20Point%20
    Processing Record 108 of set1 | The Squid and the Whale 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Squid%20and%20the%20Whale%20
    Processing Record 109 of set1 | Syriana 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Syriana%20
    Processing Record 110 of set1 | Robert Altman
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Robert%20Altman
    Processing Record 111 of set1 | Gary Demos
    <class 'IndexError'>
    list index out of range
    Processing Record 112 of set1 | Don Hall
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Don%20Hall
    Processing Record 113 of set1 | Leonardo DiCaprio
    <class 'IndexError'>
    list index out of range
    Processing Record 114 of set1 | Ryan Gosling
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ryan%20Gosling
    Processing Record 115 of set1 | Peter O'Toole
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Peter%20O'Toole
    Processing Record 116 of set1 | Will Smith
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Will%20Smith
    Processing Record 117 of set1 | Forest Whitaker
    <class 'IndexError'>
    list index out of range
    Processing Record 118 of set1 | Alan Arkin
    <class 'IndexError'>
    list index out of range
    Processing Record 119 of set1 | Jackie Earle Haley
    <class 'IndexError'>
    list index out of range
    Processing Record 120 of set1 | Djimon Hounsou
    <class 'IndexError'>
    list index out of range
    Processing Record 121 of set1 | Eddie Murphy
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Eddie%20Murphy
    Processing Record 122 of set1 | Mark Wahlberg
    <class 'IndexError'>
    list index out of range
    Processing Record 123 of set1 | Penélope Cruz
    <class 'IndexError'>
    list index out of range
    Processing Record 124 of set1 | Judi Dench
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Judi%20Dench
    Processing Record 125 of set1 | Helen Mirren
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Helen%20Mirren
    Processing Record 126 of set1 | Meryl Streep
    <class 'IndexError'>
    list index out of range
    Processing Record 127 of set1 | Kate Winslet
    <class 'IndexError'>
    list index out of range
    Processing Record 128 of set1 | Adriana Barraza
    <class 'IndexError'>
    list index out of range
    Processing Record 129 of set1 | Cate Blanchett
    <class 'IndexError'>
    list index out of range
    Processing Record 130 of set1 | Abigail Breslin
    <class 'IndexError'>
    list index out of range
    Processing Record 131 of set1 | Jennifer Hudson
    <class 'IndexError'>
    list index out of range
    Processing Record 132 of set1 | Rinko Kikuchi
    <class 'IndexError'>
    list index out of range
    Processing Record 133 of set1 | Cars 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Cars%20
    Processing Record 134 of set1 | Happy Feet 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Happy%20Feet%20
    Processing Record 135 of set1 | Monster House 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Monster%20House%20
    Processing Record 136 of set1 | Dreamgirls 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dreamgirls%20
    Processing Record 137 of set1 | The Good Shepherd 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Good%20Shepherd%20
    Processing Record 138 of set1 | Pan's Labyrinth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pan's%20Labyrinth%20
    Processing Record 139 of set1 | Pirates of the Caribbean: Dead Man's Chest 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pirates%20of%20the%20Caribbean:%20Dead%20Man's%20Chest%20
    Processing Record 140 of set1 | The Prestige 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Prestige%20
    Processing Record 141 of set1 | The Black Dahlia 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Black%20Dahlia%20
    Processing Record 142 of set1 | Children of Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Children%20of%20Men%20
    Processing Record 143 of set1 | The Illusionist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Illusionist%20
    Processing Record 144 of set1 | Pan's Labyrinth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pan's%20Labyrinth%20
    Processing Record 145 of set1 | The Prestige 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Prestige%20
    Processing Record 146 of set1 | Curse of the Golden Flower 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Curse%20of%20the%20Golden%20Flower%20
    Processing Record 147 of set1 | The Devil Wears Prada 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Devil%20Wears%20Prada%20
    Processing Record 148 of set1 | Dreamgirls 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dreamgirls%20
    Processing Record 149 of set1 | Marie Antoinette 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Marie%20Antoinette%20
    Processing Record 150 of set1 | The Queen 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Queen%20
    Processing Record 151 of set1 | Babel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Babel%20
    Processing Record 152 of set1 | The Departed 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Departed%20
    Processing Record 153 of set1 | Letters from Iwo Jima 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Letters%20from%20Iwo%20Jima%20
    Processing Record 154 of set1 | The Queen 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Queen%20
    Processing Record 155 of set1 | United 93 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=United%2093%20
    Processing Record 156 of set1 | Deliver Us from Evil 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Deliver%20Us%20from%20Evil%20
    Processing Record 157 of set1 | An Inconvenient Truth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=An%20Inconvenient%20Truth%20
    Processing Record 158 of set1 | Iraq in Fragments 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Iraq%20in%20Fragments%20
    Processing Record 159 of set1 | Jesus Camp 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jesus%20Camp%20
    Processing Record 160 of set1 | My Country, My Country 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=My%20Country,%20My%20Country%20
    Processing Record 161 of set1 | The Blood of Yingzhou District 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Blood%20of%20Yingzhou%20District%20
    Processing Record 162 of set1 | Recycled Life 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Recycled%20Life%20
    Processing Record 163 of set1 | Rehearsing a Dream 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Rehearsing%20a%20Dream%20
    Processing Record 164 of set1 | Two Hands 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Two%20Hands%20
    Processing Record 165 of set1 | Babel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Babel%20
    Processing Record 166 of set1 | Blood Diamond 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Blood%20Diamond%20
    Processing Record 167 of set1 | Children of Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Children%20of%20Men%20
    Processing Record 168 of set1 | The Departed 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Departed%20
    Processing Record 169 of set1 | United 93 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=United%2093%20
    Processing Record 170 of set1 | After the Wedding 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=After%20the%20Wedding%20
    Processing Record 171 of set1 | Days of Glory (Indigènes) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Days%20of%20Glory%20(Indig%C3%A8nes)%20
    Processing Record 172 of set1 | The Lives of Others 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Lives%20of%20Others%20
    Processing Record 173 of set1 | Pan's Labyrinth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pan's%20Labyrinth%20
    Processing Record 174 of set1 | Water 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Water%20
    Processing Record 175 of set1 | Apocalypto 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Apocalypto%20
    Processing Record 176 of set1 | Click 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Click%20
    Processing Record 177 of set1 | Pan's Labyrinth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pan's%20Labyrinth%20
    Processing Record 178 of set1 | Babel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Babel%20
    Processing Record 179 of set1 | The Good German 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Good%20German%20
    Processing Record 180 of set1 | Notes on a Scandal 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Notes%20on%20a%20Scandal%20
    Processing Record 181 of set1 | Pan's Labyrinth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pan's%20Labyrinth%20
    Processing Record 182 of set1 | The Queen 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Queen%20
    Processing Record 183 of set1 | "I Need To Wake Up" from An Inconvenient Truth
    <class 'IndexError'>
    list index out of range
    Processing Record 184 of set1 | "Listen" from Dreamgirls
    <class 'IndexError'>
    list index out of range
    Processing Record 185 of set1 | "Love You I Do" from Dreamgirls
    <class 'IndexError'>
    list index out of range
    Processing Record 186 of set1 | "Our Town" from Cars
    <class 'IndexError'>
    list index out of range
    Processing Record 187 of set1 | "Patience" from Dreamgirls
    <class 'IndexError'>
    list index out of range
    Processing Record 188 of set1 | Babel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Babel%20
    Processing Record 189 of set1 | The Departed 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Departed%20
    Processing Record 190 of set1 | Letters from Iwo Jima 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Letters%20from%20Iwo%20Jima%20
    Processing Record 191 of set1 | Little Miss Sunshine 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Little%20Miss%20Sunshine%20
    Processing Record 192 of set1 | The Queen 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Queen%20
    Processing Record 193 of set1 | The Danish Poet 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Danish%20Poet%20
    Processing Record 194 of set1 | Lifted 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lifted%20
    Processing Record 195 of set1 | The Little Matchgirl 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Little%20Matchgirl%20
    Processing Record 196 of set1 | Maestro 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Maestro%20
    Processing Record 197 of set1 | No Time for Nuts 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Time%20for%20Nuts%20
    Processing Record 198 of set1 | Binta and the Great Idea (Binta Y La Gran Idea) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Binta%20and%20the%20Great%20Idea%20(Binta%20Y%20La%20Gran%20Idea)%20
    Processing Record 199 of set1 | Éramos Pocos (One Too Many) 
    <class 'IndexError'>
    list index out of range
    Processing Record 200 of set1 | Helmer & Son 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Helmer%20&%20Son%20
    Processing Record 201 of set1 | The Saviour 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Saviour%20
    Processing Record 202 of set1 | West Bank Story 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=West%20Bank%20Story%20
    Processing Record 203 of set1 | Apocalypto 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Apocalypto%20
    Processing Record 204 of set1 | Blood Diamond 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Blood%20Diamond%20
    Processing Record 205 of set1 | Flags of Our Fathers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Flags%20of%20Our%20Fathers%20
    Processing Record 206 of set1 | Letters from Iwo Jima 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Letters%20from%20Iwo%20Jima%20
    Processing Record 207 of set1 | Pirates of the Caribbean: Dead Man's Chest 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pirates%20of%20the%20Caribbean:%20Dead%20Man's%20Chest%20
    Processing Record 208 of set1 | Apocalypto 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Apocalypto%20
    Processing Record 209 of set1 | Blood Diamond 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Blood%20Diamond%20
    Processing Record 210 of set1 | Dreamgirls 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dreamgirls%20
    Processing Record 211 of set1 | Flags of Our Fathers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Flags%20of%20Our%20Fathers%20
    Processing Record 212 of set1 | Pirates of the Caribbean: Dead Man's Chest 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pirates%20of%20the%20Caribbean:%20Dead%20Man's%20Chest%20
    Processing Record 213 of set1 | Pirates of the Caribbean: Dead Man's Chest 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pirates%20of%20the%20Caribbean:%20Dead%20Man's%20Chest%20
    Processing Record 214 of set1 | Poseidon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Poseidon%20
    Processing Record 215 of set1 | Superman Returns 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Superman%20Returns%20
    Processing Record 216 of set1 | Borat Cultural Learnings of America for Make Benefit Glorious Nation of Kazakhstan 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Borat%20Cultural%20Learnings%20of%20America%20for%20Make%20Benefit%20Glorious%20Nation%20of%20Kazakhstan%20
    Processing Record 217 of set1 | Children of Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Children%20of%20Men%20
    Processing Record 218 of set1 | The Departed 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Departed%20
    Processing Record 219 of set1 | Little Children 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Little%20Children%20
    Processing Record 220 of set1 | Notes on a Scandal 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Notes%20on%20a%20Scandal%20
    Processing Record 221 of set1 | Babel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Babel%20
    Processing Record 222 of set1 | Letters from Iwo Jima 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Letters%20from%20Iwo%20Jima%20
    Processing Record 223 of set1 | Little Miss Sunshine 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Little%20Miss%20Sunshine%20
    Processing Record 224 of set1 | Pan's Labyrinth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pan's%20Labyrinth%20
    Processing Record 225 of set1 | The Queen 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Queen%20
    Processing Record 226 of set1 | Sherry Lansing
    <class 'IndexError'>
    list index out of range
    Processing Record 227 of set1 | Ennio Morricone
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ennio%20Morricone
    Processing Record 228 of set1 | Ray Feeney
    <class 'IndexError'>
    list index out of range
    Processing Record 229 of set1 | Ioan Allen, J. Wayne Anderson, Mary Ann Anderson, Ted Costas, Paul R. Goldberg, Shawn Jones, Thomas Kuhn, Dr. Alan Masson, Colin Mossman, Martin Richards, Frank Ricotta and Richard C. Sehlin
    <class 'IndexError'>
    list index out of range
    Processing Record 230 of set1 | Richard Edlund
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Richard%20Edlund
    Processing Record 231 of set1 | George Clooney
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=George%20Clooney
    Processing Record 232 of set1 | Daniel Day-Lewis
    <class 'IndexError'>
    list index out of range
    Processing Record 233 of set1 | Johnny Depp
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Johnny%20Depp
    Processing Record 234 of set1 | Tommy Lee Jones
    <class 'IndexError'>
    list index out of range
    Processing Record 235 of set1 | Viggo Mortensen
    <class 'IndexError'>
    list index out of range
    Processing Record 236 of set1 | Casey Affleck
    <class 'IndexError'>
    list index out of range
    Processing Record 237 of set1 | Javier Bardem
    <class 'IndexError'>
    list index out of range
    Processing Record 238 of set1 | Philip Seymour Hoffman
    <class 'IndexError'>
    list index out of range
    Processing Record 239 of set1 | Hal Holbrook
    <class 'IndexError'>
    list index out of range
    Processing Record 240 of set1 | Tom Wilkinson
    <class 'IndexError'>
    list index out of range
    Processing Record 1 of set2 | Cate Blanchett
    <class 'IndexError'>
    list index out of range
    Processing Record 2 of set2 | Julie Christie
    <class 'IndexError'>
    list index out of range
    Processing Record 3 of set2 | Marion Cotillard
    <class 'IndexError'>
    list index out of range
    Processing Record 4 of set2 | Laura Linney
    <class 'IndexError'>
    list index out of range
    Processing Record 5 of set2 | Ellen Page
    <class 'IndexError'>
    list index out of range
    Processing Record 6 of set2 | Cate Blanchett
    <class 'IndexError'>
    list index out of range
    Processing Record 7 of set2 | Ruby Dee
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ruby%20Dee
    Processing Record 8 of set2 | Saoirse Ronan
    <class 'IndexError'>
    list index out of range
    Processing Record 9 of set2 | Amy Ryan
    <class 'IndexError'>
    list index out of range
    Processing Record 10 of set2 | Tilda Swinton
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tilda%20Swinton
    Processing Record 11 of set2 | Persepolis 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Persepolis%20
    Processing Record 12 of set2 | Ratatouille 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ratatouille%20
    Processing Record 13 of set2 | Surf's Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Surf's%20Up%20
    Processing Record 14 of set2 | American Gangster 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Gangster%20
    Processing Record 15 of set2 | Atonement 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Atonement%20
    Processing Record 16 of set2 | The Golden Compass 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Golden%20Compass%20
    Processing Record 17 of set2 | Sweeney Todd The Demon Barber of Fleet Street 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sweeney%20Todd%20The%20Demon%20Barber%20of%20Fleet%20Street%20
    Processing Record 18 of set2 | There Will Be Blood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=There%20Will%20Be%20Blood%20
    Processing Record 19 of set2 | The Assassination of Jesse James by the Coward Robert Ford 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Assassination%20of%20Jesse%20James%20by%20the%20Coward%20Robert%20Ford%20
    Processing Record 20 of set2 | Atonement 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Atonement%20
    Processing Record 21 of set2 | The Diving Bell and the Butterfly 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Diving%20Bell%20and%20the%20Butterfly%20
    Processing Record 22 of set2 | No Country for Old Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Country%20for%20Old%20Men%20
    Processing Record 23 of set2 | There Will Be Blood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=There%20Will%20Be%20Blood%20
    Processing Record 24 of set2 | Across the Universe 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Across%20the%20Universe%20
    Processing Record 25 of set2 | Atonement 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Atonement%20
    Processing Record 26 of set2 | Elizabeth: The Golden Age 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Elizabeth:%20The%20Golden%20Age%20
    Processing Record 27 of set2 | La Vie en Rose 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=La%20Vie%20en%20Rose%20
    Processing Record 28 of set2 | Sweeney Todd The Demon Barber of Fleet Street 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sweeney%20Todd%20The%20Demon%20Barber%20of%20Fleet%20Street%20
    Processing Record 29 of set2 | The Diving Bell and the Butterfly 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Diving%20Bell%20and%20the%20Butterfly%20
    Processing Record 30 of set2 | Juno 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Juno%20
    Processing Record 31 of set2 | Michael Clayton 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Michael%20Clayton%20
    Processing Record 32 of set2 | No Country for Old Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Country%20for%20Old%20Men%20
    Processing Record 33 of set2 | There Will Be Blood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=There%20Will%20Be%20Blood%20
    Processing Record 34 of set2 | No End in Sight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20End%20in%20Sight%20
    Processing Record 35 of set2 | Operation Homecoming: Writing the Wartime Experience 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Operation%20Homecoming:%20Writing%20the%20Wartime%20Experience%20
    Processing Record 36 of set2 | Sicko 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sicko%20
    Processing Record 37 of set2 | Taxi to the Dark Side 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Taxi%20to%20the%20Dark%20Side%20
    Processing Record 38 of set2 | War/Dance 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War/Dance%20
    Processing Record 39 of set2 | Freeheld 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Freeheld%20
    Processing Record 40 of set2 | La Corona (The Crown) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=La%20Corona%20(The%20Crown)%20
    Processing Record 41 of set2 | Salim Baba 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Salim%20Baba%20
    Processing Record 42 of set2 | Sari's Mother 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sari's%20Mother%20
    Processing Record 43 of set2 | The Bourne Ultimatum 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Bourne%20Ultimatum%20
    Processing Record 44 of set2 | The Diving Bell and the Butterfly 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Diving%20Bell%20and%20the%20Butterfly%20
    Processing Record 45 of set2 | Into the Wild 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Into%20the%20Wild%20
    Processing Record 46 of set2 | No Country for Old Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Country%20for%20Old%20Men%20
    Processing Record 47 of set2 | There Will Be Blood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=There%20Will%20Be%20Blood%20
    Processing Record 48 of set2 | Beaufort 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Beaufort%20
    Processing Record 49 of set2 | The Counterfeiters 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Counterfeiters%20
    Processing Record 50 of set2 | Katyn 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Katyn%20
    Processing Record 51 of set2 | Mongol 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mongol%20
    Processing Record 52 of set2 | 12
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=12
    Processing Record 53 of set2 | La Vie en Rose 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=La%20Vie%20en%20Rose%20
    Processing Record 54 of set2 | Norbit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Norbit%20
    Processing Record 55 of set2 | Pirates of the Caribbean: At World's End 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pirates%20of%20the%20Caribbean:%20At%20World's%20End%20
    Processing Record 56 of set2 | Atonement 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Atonement%20
    Processing Record 57 of set2 | The Kite Runner 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Kite%20Runner%20
    Processing Record 58 of set2 | Michael Clayton 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Michael%20Clayton%20
    Processing Record 59 of set2 | Ratatouille 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ratatouille%20
    Processing Record 60 of set2 | 3:10 to Yuma 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=3:10%20to%20Yuma%20
    Processing Record 61 of set2 | "Falling Slowly" from Once
    <class 'IndexError'>
    list index out of range
    Processing Record 62 of set2 | "Happy Working Song" from Enchanted
    <class 'IndexError'>
    list index out of range
    Processing Record 63 of set2 | "Raise It Up" from August Rush
    <class 'IndexError'>
    list index out of range
    Processing Record 64 of set2 | "So Close" from Enchanted
    <class 'IndexError'>
    list index out of range
    Processing Record 65 of set2 | "That's How You Know" from Enchanted
    <class 'IndexError'>
    list index out of range
    Processing Record 66 of set2 | Atonement 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Atonement%20
    Processing Record 67 of set2 | Juno 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Juno%20
    Processing Record 68 of set2 | Michael Clayton 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Michael%20Clayton%20
    Processing Record 69 of set2 | No Country for Old Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Country%20for%20Old%20Men%20
    Processing Record 70 of set2 | There Will Be Blood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=There%20Will%20Be%20Blood%20
    Processing Record 71 of set2 | I Met the Walrus 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=I%20Met%20the%20Walrus%20
    Processing Record 72 of set2 | Madame Tutli-Putli 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Madame%20Tutli-Putli%20
    Processing Record 73 of set2 | Même les Pigeons Vont au Paradis (Even Pigeons Go to Heaven) 
    <class 'IndexError'>
    list index out of range
    Processing Record 74 of set2 | My Love (Moya Lyubov) 
    <class 'IndexError'>
    list index out of range
    Processing Record 75 of set2 | Peter & the Wolf 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Peter%20&%20the%20Wolf%20
    Processing Record 76 of set2 | At Night 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=At%20Night%20
    Processing Record 77 of set2 | Il Supplente (The Substitute) 
    <class 'IndexError'>
    list index out of range
    Processing Record 78 of set2 | Le Mozart des Pickpockets (The Mozart of Pickpockets) 
    <class 'IndexError'>
    list index out of range
    Processing Record 79 of set2 | Tanghi Argentini 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tanghi%20Argentini%20
    Processing Record 80 of set2 | The Tonto Woman 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Tonto%20Woman%20
    Processing Record 81 of set2 | The Bourne Ultimatum 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Bourne%20Ultimatum%20
    Processing Record 82 of set2 | No Country for Old Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Country%20for%20Old%20Men%20
    Processing Record 83 of set2 | Ratatouille 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ratatouille%20
    Processing Record 84 of set2 | There Will Be Blood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=There%20Will%20Be%20Blood%20
    Processing Record 85 of set2 | Transformers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Transformers%20
    Processing Record 86 of set2 | The Bourne Ultimatum 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Bourne%20Ultimatum%20
    Processing Record 87 of set2 | No Country for Old Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Country%20for%20Old%20Men%20
    Processing Record 88 of set2 | Ratatouille 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ratatouille%20
    Processing Record 89 of set2 | 3:10 to Yuma 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=3:10%20to%20Yuma%20
    Processing Record 90 of set2 | Transformers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Transformers%20
    Processing Record 91 of set2 | The Golden Compass 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Golden%20Compass%20
    Processing Record 92 of set2 | Pirates of the Caribbean: At World's End 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pirates%20of%20the%20Caribbean:%20At%20World's%20End%20
    Processing Record 93 of set2 | Transformers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Transformers%20
    Processing Record 94 of set2 | Atonement 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Atonement%20
    Processing Record 95 of set2 | Away from Her 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Away%20from%20Her%20
    Processing Record 96 of set2 | The Diving Bell and the Butterfly 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Diving%20Bell%20and%20the%20Butterfly%20
    Processing Record 97 of set2 | No Country for Old Men 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20Country%20for%20Old%20Men%20
    Processing Record 98 of set2 | There Will Be Blood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=There%20Will%20Be%20Blood%20
    Processing Record 99 of set2 | Juno 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Juno%20
    Processing Record 100 of set2 | Lars and the Real Girl 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lars%20and%20the%20Real%20Girl%20
    Processing Record 101 of set2 | Michael Clayton 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Michael%20Clayton%20
    Processing Record 102 of set2 | Ratatouille 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ratatouille%20
    Processing Record 103 of set2 | The Savages 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Savages%20
    Processing Record 104 of set2 | Robert Boyle
    <class 'IndexError'>
    list index out of range
    Processing Record 105 of set2 | David A. Grafton
    <class 'IndexError'>
    list index out of range
    Processing Record 106 of set2 | Jonathan Erland
    <class 'IndexError'>
    list index out of range
    Processing Record 107 of set2 | David Inglish
    <class 'IndexError'>
    list index out of range
    Processing Record 108 of set2 | Richard Jenkins
    <class 'IndexError'>
    list index out of range
    Processing Record 109 of set2 | Frank Langella
    <class 'IndexError'>
    list index out of range
    Processing Record 110 of set2 | Sean Penn
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sean%20Penn
    Processing Record 111 of set2 | Brad Pitt
    <class 'IndexError'>
    list index out of range
    Processing Record 112 of set2 | Mickey Rourke
    <class 'IndexError'>
    list index out of range
    Processing Record 113 of set2 | Josh Brolin
    <class 'IndexError'>
    list index out of range
    Processing Record 114 of set2 | Robert Downey Jr.
    <class 'IndexError'>
    list index out of range
    Processing Record 115 of set2 | Philip Seymour Hoffman
    <class 'IndexError'>
    list index out of range
    Processing Record 116 of set2 | Heath Ledger
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Heath%20Ledger
    Processing Record 117 of set2 | Michael Shannon
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Michael%20Shannon
    Processing Record 118 of set2 | Anne Hathaway
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anne%20Hathaway
    Processing Record 119 of set2 | Angelina Jolie
    <class 'IndexError'>
    list index out of range
    Processing Record 120 of set2 | Melissa Leo
    <class 'IndexError'>
    list index out of range
    Processing Record 121 of set2 | Meryl Streep
    <class 'IndexError'>
    list index out of range
    Processing Record 122 of set2 | Kate Winslet
    <class 'IndexError'>
    list index out of range
    Processing Record 123 of set2 | Amy Adams
    <class 'IndexError'>
    list index out of range
    Processing Record 124 of set2 | Penélope Cruz
    <class 'IndexError'>
    list index out of range
    Processing Record 125 of set2 | Viola Davis
    <class 'IndexError'>
    list index out of range
    Processing Record 126 of set2 | Taraji P. Henson
    <class 'IndexError'>
    list index out of range
    Processing Record 127 of set2 | Marisa Tomei
    <class 'IndexError'>
    list index out of range
    Processing Record 128 of set2 | Bolt 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bolt%20
    Processing Record 129 of set2 | Kung Fu Panda 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Kung%20Fu%20Panda%20
    Processing Record 130 of set2 | WALL-E 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=WALL-E%20
    Processing Record 131 of set2 | Changeling 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Changeling%20
    Processing Record 132 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 133 of set2 | The Dark Knight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dark%20Knight%20
    Processing Record 134 of set2 | The Duchess 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Duchess%20
    Processing Record 135 of set2 | Revolutionary Road 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Revolutionary%20Road%20
    Processing Record 136 of set2 | Changeling 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Changeling%20
    Processing Record 137 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 138 of set2 | The Dark Knight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dark%20Knight%20
    Processing Record 139 of set2 | The Reader 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Reader%20
    Processing Record 140 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 141 of set2 | Australia 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Australia%20
    Processing Record 142 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 143 of set2 | The Duchess 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Duchess%20
    Processing Record 144 of set2 | Milk 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Milk%20
    Processing Record 145 of set2 | Revolutionary Road 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Revolutionary%20Road%20
    Processing Record 146 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 147 of set2 | Frost/Nixon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Frost/Nixon%20
    Processing Record 148 of set2 | Milk 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Milk%20
    Processing Record 149 of set2 | The Reader 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Reader%20
    Processing Record 150 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 151 of set2 | The Betrayal (Nerakhoon) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Betrayal%20(Nerakhoon)%20
    Processing Record 152 of set2 | Encounters at the End of the World 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Encounters%20at%20the%20End%20of%20the%20World%20
    Processing Record 153 of set2 | The Garden 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Garden%20
    Processing Record 154 of set2 | Man on Wire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Man%20on%20Wire%20
    Processing Record 155 of set2 | Trouble the Water 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Trouble%20the%20Water%20
    Processing Record 156 of set2 | The Conscience of Nhem En 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Conscience%20of%20Nhem%20En%20
    Processing Record 157 of set2 | The Final Inch 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Final%20Inch%20
    Processing Record 158 of set2 | Smile Pinki 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Smile%20Pinki%20
    Processing Record 159 of set2 | The Witness - From the Balcony of Room 306 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Witness%20-%20From%20the%20Balcony%20of%20Room%20306%20
    Processing Record 160 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 161 of set2 | The Dark Knight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dark%20Knight%20
    Processing Record 162 of set2 | Frost/Nixon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Frost/Nixon%20
    Processing Record 163 of set2 | Milk 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Milk%20
    Processing Record 164 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 165 of set2 | The Baader Meinhof Complex 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Baader%20Meinhof%20Complex%20
    Processing Record 166 of set2 | The Class 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Class%20
    Processing Record 167 of set2 | Departures 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Departures%20
    Processing Record 168 of set2 | Revanche 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Revanche%20
    Processing Record 169 of set2 | Waltz with Bashir 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Waltz%20with%20Bashir%20
    Processing Record 170 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 171 of set2 | The Dark Knight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dark%20Knight%20
    Processing Record 172 of set2 | Hellboy II: The Golden Army 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hellboy%20II:%20The%20Golden%20Army%20
    Processing Record 173 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 174 of set2 | Defiance 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Defiance%20
    Processing Record 175 of set2 | Milk 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Milk%20
    Processing Record 176 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 177 of set2 | WALL-E 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=WALL-E%20
    Processing Record 178 of set2 | "Down To Earth" from WALL-E
    <class 'IndexError'>
    list index out of range
    Processing Record 179 of set2 | "Jai Ho" from Slumdog Millionaire
    <class 'IndexError'>
    list index out of range
    Processing Record 180 of set2 | "O Saya" from Slumdog Millionaire
    <class 'IndexError'>
    list index out of range
    Processing Record 181 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 182 of set2 | Frost/Nixon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Frost/Nixon%20
    Processing Record 183 of set2 | Milk 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Milk%20
    Processing Record 184 of set2 | The Reader 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Reader%20
    Processing Record 185 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 186 of set2 | La Maison en Petits Cubes 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=La%20Maison%20en%20Petits%20Cubes%20
    Processing Record 187 of set2 | Lavatory - Lovestory 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lavatory%20-%20Lovestory%20
    Processing Record 188 of set2 | Oktapodi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Oktapodi%20
    Processing Record 189 of set2 | Presto 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Presto%20
    Processing Record 190 of set2 | This Way Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=This%20Way%20Up%20
    Processing Record 191 of set2 | Auf der Strecke (On the Line) 
    <class 'IndexError'>
    list index out of range
    Processing Record 192 of set2 | Manon on the Asphalt 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Manon%20on%20the%20Asphalt%20
    Processing Record 193 of set2 | New Boy 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=New%20Boy%20
    Processing Record 194 of set2 | The Pig 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Pig%20
    Processing Record 195 of set2 | Spielzeugland (Toyland) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Spielzeugland%20(Toyland)%20
    Processing Record 196 of set2 | The Dark Knight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dark%20Knight%20
    Processing Record 197 of set2 | Iron Man 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Iron%20Man%20
    Processing Record 198 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 199 of set2 | WALL-E 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=WALL-E%20
    Processing Record 200 of set2 | Wanted 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Wanted%20
    Processing Record 201 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 202 of set2 | The Dark Knight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dark%20Knight%20
    Processing Record 203 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 204 of set2 | WALL-E 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=WALL-E%20
    Processing Record 205 of set2 | Wanted 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Wanted%20
    Processing Record 206 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 207 of set2 | The Dark Knight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dark%20Knight%20
    Processing Record 208 of set2 | Iron Man 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Iron%20Man%20
    Processing Record 209 of set2 | The Curious Case of Benjamin Button 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Curious%20Case%20of%20Benjamin%20Button%20
    Processing Record 210 of set2 | Doubt 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Doubt%20
    Processing Record 211 of set2 | Frost/Nixon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Frost/Nixon%20
    Processing Record 212 of set2 | The Reader 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Reader%20
    Processing Record 213 of set2 | Slumdog Millionaire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Slumdog%20Millionaire%20
    Processing Record 214 of set2 | Frozen River 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Frozen%20River%20
    Processing Record 215 of set2 | Happy-Go-Lucky 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Happy-Go-Lucky%20
    Processing Record 216 of set2 | In Bruges 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=In%20Bruges%20
    Processing Record 217 of set2 | Milk 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Milk%20
    Processing Record 218 of set2 | WALL-E 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=WALL-E%20
    Processing Record 219 of set2 | Jerry Lewis
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jerry%20Lewis
    Processing Record 220 of set2 | Ed Catmull
    <class 'IndexError'>
    list index out of range
    Processing Record 221 of set2 | Mark Kimball
    <class 'IndexError'>
    list index out of range
    Processing Record 222 of set2 | Jeff Bridges
    <class 'IndexError'>
    list index out of range
    Processing Record 223 of set2 | George Clooney
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=George%20Clooney
    Processing Record 224 of set2 | Colin Firth
    <class 'IndexError'>
    list index out of range
    Processing Record 225 of set2 | Morgan Freeman
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Morgan%20Freeman
    Processing Record 226 of set2 | Jeremy Renner
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jeremy%20Renner
    Processing Record 227 of set2 | Matt Damon
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Matt%20Damon
    Processing Record 228 of set2 | Woody Harrelson
    <class 'IndexError'>
    list index out of range
    Processing Record 229 of set2 | Christopher Plummer
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Christopher%20Plummer
    Processing Record 230 of set2 | Stanley Tucci
    <class 'IndexError'>
    list index out of range
    Processing Record 231 of set2 | Christoph Waltz
    <class 'IndexError'>
    list index out of range
    Processing Record 232 of set2 | Sandra Bullock
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sandra%20Bullock
    Processing Record 233 of set2 | Helen Mirren
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Helen%20Mirren
    Processing Record 234 of set2 | Carey Mulligan
    <class 'IndexError'>
    list index out of range
    Processing Record 235 of set2 | Gabourey Sidibe
    <class 'IndexError'>
    list index out of range
    Processing Record 236 of set2 | Meryl Streep
    <class 'IndexError'>
    list index out of range
    Processing Record 237 of set2 | Penélope Cruz
    <class 'IndexError'>
    list index out of range
    Processing Record 238 of set2 | Vera Farmiga
    <class 'IndexError'>
    list index out of range
    Processing Record 239 of set2 | Maggie Gyllenhaal
    <class 'IndexError'>
    list index out of range
    Processing Record 240 of set2 | Anna Kendrick
    <class 'IndexError'>
    list index out of range
    Processing Record 1 of set3 | Mo'Nique
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mo'Nique
    Processing Record 2 of set3 | Coraline 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Coraline%20
    Processing Record 3 of set3 | Fantastic Mr. Fox 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Fantastic%20Mr.%20Fox%20
    Processing Record 4 of set3 | The Princess and the Frog 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Princess%20and%20the%20Frog%20
    Processing Record 5 of set3 | The Secret of Kells 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Secret%20of%20Kells%20
    Processing Record 6 of set3 | Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20
    Processing Record 7 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 8 of set3 | The Imaginarium of Doctor Parnassus 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imaginarium%20of%20Doctor%20Parnassus%20
    Processing Record 9 of set3 | Nine 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nine%20
    Processing Record 10 of set3 | Sherlock Holmes 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sherlock%20Holmes%20
    Processing Record 11 of set3 | The Young Victoria 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Young%20Victoria%20
    Processing Record 12 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 13 of set3 | Harry Potter and the Half-Blood Prince 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Potter%20and%20the%20Half-Blood%20Prince%20
    Processing Record 14 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 15 of set3 | Inglourious Basterds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inglourious%20Basterds%20
    Processing Record 16 of set3 | The White Ribbon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20White%20Ribbon%20
    Processing Record 17 of set3 | Bright Star 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bright%20Star%20
    Processing Record 18 of set3 | Coco before Chanel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Coco%20before%20Chanel%20
    Processing Record 19 of set3 | The Imaginarium of Doctor Parnassus 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imaginarium%20of%20Doctor%20Parnassus%20
    Processing Record 20 of set3 | Nine 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nine%20
    Processing Record 21 of set3 | The Young Victoria 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Young%20Victoria%20
    Processing Record 22 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 23 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 24 of set3 | Inglourious Basterds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inglourious%20Basterds%20
    Processing Record 25 of set3 | Precious: Based on the Novel 'Push' by Sapphire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Precious:%20Based%20on%20the%20Novel%20'Push'%20by%20Sapphire%20
    Processing Record 26 of set3 | Up in the Air 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20in%20the%20Air%20
    Processing Record 27 of set3 | Burma VJ 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Burma%20VJ%20
    Processing Record 28 of set3 | The Cove 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Cove%20
    Processing Record 29 of set3 | Food, Inc. 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Food,%20Inc.%20
    Processing Record 30 of set3 | The Most Dangerous Man in America: Daniel Ellsberg and the Pentagon Papers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Most%20Dangerous%20Man%20in%20America:%20Daniel%20Ellsberg%20and%20the%20Pentagon%20Papers%20
    Processing Record 31 of set3 | Which Way Home 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Which%20Way%20Home%20
    Processing Record 32 of set3 | China's Unnatural Disaster: The Tears of Sichuan Province 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=China's%20Unnatural%20Disaster:%20The%20Tears%20of%20Sichuan%20Province%20
    Processing Record 33 of set3 | The Last Campaign of Governor Booth Gardner 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Last%20Campaign%20of%20Governor%20Booth%20Gardner%20
    Processing Record 34 of set3 | The Last Truck: Closing of a GM Plant 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Last%20Truck:%20Closing%20of%20a%20GM%20Plant%20
    Processing Record 35 of set3 | Music by Prudence 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Music%20by%20Prudence%20
    Processing Record 36 of set3 | Rabbit à la Berlin 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Rabbit%20%C3%A0%20la%20Berlin%20
    Processing Record 37 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 38 of set3 | District 9 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=District%209%20
    Processing Record 39 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 40 of set3 | Inglourious Basterds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inglourious%20Basterds%20
    Processing Record 41 of set3 | Precious: Based on the Novel 'Push' by Sapphire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Precious:%20Based%20on%20the%20Novel%20'Push'%20by%20Sapphire%20
    Processing Record 42 of set3 | Ajami 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ajami%20
    Processing Record 43 of set3 | The Milk of Sorrow 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Milk%20of%20Sorrow%20
    Processing Record 44 of set3 | A Prophet 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Prophet%20
    Processing Record 45 of set3 | The Secret in Their Eyes 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Secret%20in%20Their%20Eyes%20
    Processing Record 46 of set3 | The White Ribbon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20White%20Ribbon%20
    Processing Record 47 of set3 | Il Divo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Il%20Divo%20
    Processing Record 48 of set3 | Star Trek 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Trek%20
    Processing Record 49 of set3 | The Young Victoria 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Young%20Victoria%20
    Processing Record 50 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 51 of set3 | Fantastic Mr. Fox 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Fantastic%20Mr.%20Fox%20
    Processing Record 52 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 53 of set3 | Sherlock Holmes 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sherlock%20Holmes%20
    Processing Record 54 of set3 | Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20
    Processing Record 55 of set3 | "Almost There" from The Princess and the Frog
    <class 'IndexError'>
    list index out of range
    Processing Record 56 of set3 | "Down In New Orleans" from The Princess and the Frog
    <class 'IndexError'>
    list index out of range
    Processing Record 57 of set3 | "Loin De Paname" from Paris 36
    <class 'IndexError'>
    list index out of range
    Processing Record 58 of set3 | "Take It All" from Nine
    <class 'IndexError'>
    list index out of range
    Processing Record 59 of set3 | "The Weary Kind (Theme From Crazy Heart)" from Crazy Heart
    <class 'IndexError'>
    list index out of range
    Processing Record 60 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 61 of set3 | The Blind Side 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Blind%20Side%20
    Processing Record 62 of set3 | District 9 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=District%209%20
    Processing Record 63 of set3 | An Education 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=An%20Education%20
    Processing Record 64 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 65 of set3 | Inglourious Basterds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inglourious%20Basterds%20
    Processing Record 66 of set3 | Precious: Based on the Novel 'Push' by Sapphire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Precious:%20Based%20on%20the%20Novel%20'Push'%20by%20Sapphire%20
    Processing Record 67 of set3 | A Serious Man 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Serious%20Man%20
    Processing Record 68 of set3 | Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20
    Processing Record 69 of set3 | Up in the Air 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20in%20the%20Air%20
    Processing Record 70 of set3 | French Roast 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=French%20Roast%20
    Processing Record 71 of set3 | Granny O'Grimm's Sleeping Beauty 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Granny%20O'Grimm's%20Sleeping%20Beauty%20
    Processing Record 72 of set3 | The Lady and the Reaper (La Dama y la Muerte) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Lady%20and%20the%20Reaper%20(La%20Dama%20y%20la%20Muerte)%20
    Processing Record 73 of set3 | Logorama 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Logorama%20
    Processing Record 74 of set3 | A Matter of Loaf and Death 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Matter%20of%20Loaf%20and%20Death%20
    Processing Record 75 of set3 | The Door 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Door%20
    Processing Record 76 of set3 | Instead of Abracadabra 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Instead%20of%20Abracadabra%20
    Processing Record 77 of set3 | Kavi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Kavi%20
    Processing Record 78 of set3 | Miracle Fish 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Miracle%20Fish%20
    Processing Record 79 of set3 | The New Tenants 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20New%20Tenants%20
    Processing Record 80 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 81 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 82 of set3 | Inglourious Basterds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inglourious%20Basterds%20
    Processing Record 83 of set3 | Star Trek 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Trek%20
    Processing Record 84 of set3 | Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20
    Processing Record 85 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 86 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 87 of set3 | Inglourious Basterds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inglourious%20Basterds%20
    Processing Record 88 of set3 | Star Trek 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Trek%20
    Processing Record 89 of set3 | Transformers: Revenge of the Fallen 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Transformers:%20Revenge%20of%20the%20Fallen%20
    Processing Record 90 of set3 | Avatar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avatar%20
    Processing Record 91 of set3 | District 9 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=District%209%20
    Processing Record 92 of set3 | Star Trek 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Trek%20
    Processing Record 93 of set3 | District 9 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=District%209%20
    Processing Record 94 of set3 | An Education 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=An%20Education%20
    Processing Record 95 of set3 | In the Loop 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=In%20the%20Loop%20
    Processing Record 96 of set3 | Precious: Based on the Novel 'Push' by Sapphire 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Precious:%20Based%20on%20the%20Novel%20'Push'%20by%20Sapphire%20
    Processing Record 97 of set3 | Up in the Air 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20in%20the%20Air%20
    Processing Record 98 of set3 | The Hurt Locker 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hurt%20Locker%20
    Processing Record 99 of set3 | Inglourious Basterds 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inglourious%20Basterds%20
    Processing Record 100 of set3 | The Messenger 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Messenger%20
    Processing Record 101 of set3 | A Serious Man 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Serious%20Man%20
    Processing Record 102 of set3 | Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Up%20
    Processing Record 103 of set3 | Lauren Bacall
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lauren%20Bacall
    Processing Record 104 of set3 | Roger Corman
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Roger%20Corman
    Processing Record 105 of set3 | Gordon Willis
    <class 'IndexError'>
    list index out of range
    Processing Record 106 of set3 | John Calley
    <class 'IndexError'>
    list index out of range
    Processing Record 107 of set3 | Javier Bardem
    <class 'IndexError'>
    list index out of range
    Processing Record 108 of set3 | Jeff Bridges
    <class 'IndexError'>
    list index out of range
    Processing Record 109 of set3 | Jesse Eisenberg
    <class 'IndexError'>
    list index out of range
    Processing Record 110 of set3 | Colin Firth
    <class 'IndexError'>
    list index out of range
    Processing Record 111 of set3 | James Franco
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=James%20Franco
    Processing Record 112 of set3 | Christian Bale
    <class 'IndexError'>
    list index out of range
    Processing Record 113 of set3 | John Hawkes
    <class 'IndexError'>
    list index out of range
    Processing Record 114 of set3 | Jeremy Renner
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jeremy%20Renner
    Processing Record 115 of set3 | Mark Ruffalo
    <class 'IndexError'>
    list index out of range
    Processing Record 116 of set3 | Geoffrey Rush
    <class 'IndexError'>
    list index out of range
    Processing Record 117 of set3 | Annette Bening
    <class 'IndexError'>
    list index out of range
    Processing Record 118 of set3 | Nicole Kidman
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nicole%20Kidman
    Processing Record 119 of set3 | Jennifer Lawrence
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jennifer%20Lawrence
    Processing Record 120 of set3 | Natalie Portman
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Natalie%20Portman
    Processing Record 121 of set3 | Michelle Williams
    <class 'IndexError'>
    list index out of range
    Processing Record 122 of set3 | Amy Adams
    <class 'IndexError'>
    list index out of range
    Processing Record 123 of set3 | Helena Bonham Carter
    <class 'IndexError'>
    list index out of range
    Processing Record 124 of set3 | Melissa Leo
    <class 'IndexError'>
    list index out of range
    Processing Record 125 of set3 | Hailee Steinfeld
    <class 'IndexError'>
    list index out of range
    Processing Record 126 of set3 | Jacki Weaver
    <class 'IndexError'>
    list index out of range
    Processing Record 127 of set3 | How to Train Your Dragon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=How%20to%20Train%20Your%20Dragon%20
    Processing Record 128 of set3 | The Illusionist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Illusionist%20
    Processing Record 129 of set3 | Toy Story 3 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Toy%20Story%203%20
    Processing Record 130 of set3 | Alice in Wonderland 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Alice%20in%20Wonderland%20
    Processing Record 131 of set3 | Harry Potter and the Deathly Hallows Part 1 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Potter%20and%20the%20Deathly%20Hallows%20Part%201%20
    Processing Record 132 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 133 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 134 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 135 of set3 | Black Swan 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Black%20Swan%20
    Processing Record 136 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 137 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 138 of set3 | The Social Network 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Social%20Network%20
    Processing Record 139 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 140 of set3 | Alice in Wonderland 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Alice%20in%20Wonderland%20
    Processing Record 141 of set3 | I Am Love 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=I%20Am%20Love%20
    Processing Record 142 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 143 of set3 | The Tempest 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Tempest%20
    Processing Record 144 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 145 of set3 | Black Swan 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Black%20Swan%20
    Processing Record 146 of set3 | The Fighter 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Fighter%20
    Processing Record 147 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 148 of set3 | The Social Network 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Social%20Network%20
    Processing Record 149 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 150 of set3 | Exit through the Gift Shop 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Exit%20through%20the%20Gift%20Shop%20
    Processing Record 151 of set3 | Gasland 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gasland%20
    Processing Record 152 of set3 | Inside Job 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inside%20Job%20
    Processing Record 153 of set3 | Restrepo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Restrepo%20
    Processing Record 154 of set3 | Waste Land 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Waste%20Land%20
    Processing Record 155 of set3 | Killing in the Name 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Killing%20in%20the%20Name%20
    Processing Record 156 of set3 | Poster Girl 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Poster%20Girl%20
    Processing Record 157 of set3 | Strangers No More 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Strangers%20No%20More%20
    Processing Record 158 of set3 | Sun Come Up 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sun%20Come%20Up%20
    Processing Record 159 of set3 | The Warriors of Qiugang 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Warriors%20of%20Qiugang%20
    Processing Record 160 of set3 | Black Swan 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Black%20Swan%20
    Processing Record 161 of set3 | The Fighter 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Fighter%20
    Processing Record 162 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 163 of set3 | 127 Hours 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=127%20Hours%20
    Processing Record 164 of set3 | The Social Network 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Social%20Network%20
    Processing Record 165 of set3 | Biutiful 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Biutiful%20
    Processing Record 166 of set3 | Dogtooth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dogtooth%20
    Processing Record 167 of set3 | In a Better World 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=In%20a%20Better%20World%20
    Processing Record 168 of set3 | Incendies 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Incendies%20
    Processing Record 169 of set3 | Outside the Law (Hors-la-loi) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Outside%20the%20Law%20(Hors-la-loi)%20
    Processing Record 170 of set3 | Barney's Version 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Barney's%20Version%20
    Processing Record 171 of set3 | The Way Back 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Way%20Back%20
    Processing Record 172 of set3 | The Wolfman 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Wolfman%20
    Processing Record 173 of set3 | How to Train Your Dragon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=How%20to%20Train%20Your%20Dragon%20
    Processing Record 174 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 175 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 176 of set3 | 127 Hours 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=127%20Hours%20
    Processing Record 177 of set3 | The Social Network 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Social%20Network%20
    Processing Record 178 of set3 | "Coming Home" from Country Strong
    <class 'IndexError'>
    list index out of range
    Processing Record 179 of set3 | "I See The Light" from Tangled
    <class 'IndexError'>
    list index out of range
    Processing Record 180 of set3 | "If I Rise" from 127 Hours
    <class 'IndexError'>
    list index out of range
    Processing Record 181 of set3 | "We Belong Together" from Toy Story 3
    <class 'IndexError'>
    list index out of range
    Processing Record 182 of set3 | Black Swan 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Black%20Swan%20
    Processing Record 183 of set3 | The Fighter 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Fighter%20
    Processing Record 184 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 185 of set3 | The Kids Are All Right 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Kids%20Are%20All%20Right%20
    Processing Record 186 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 187 of set3 | 127 Hours 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=127%20Hours%20
    Processing Record 188 of set3 | The Social Network 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Social%20Network%20
    Processing Record 189 of set3 | Toy Story 3 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Toy%20Story%203%20
    Processing Record 190 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 191 of set3 | Winter's Bone 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Winter's%20Bone%20
    Processing Record 192 of set3 | Day & Night 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Day%20&%20Night%20
    Processing Record 193 of set3 | The Gruffalo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Gruffalo%20
    Processing Record 194 of set3 | Let's Pollute 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Let's%20Pollute%20
    Processing Record 195 of set3 | The Lost Thing 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Lost%20Thing%20
    Processing Record 196 of set3 | Madagascar, carnet de voyage (Madagascar, a Journey Diary) 
    <class 'IndexError'>
    list index out of range
    Processing Record 197 of set3 | The Confession 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Confession%20
    Processing Record 198 of set3 | The Crush 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Crush%20
    Processing Record 199 of set3 | God of Love 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=God%20of%20Love%20
    Processing Record 200 of set3 | Na Wewe 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Na%20Wewe%20
    Processing Record 201 of set3 | Wish 143 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Wish%20143%20
    Processing Record 202 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 203 of set3 | Toy Story 3 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Toy%20Story%203%20
    Processing Record 204 of set3 | Tron: Legacy 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tron:%20Legacy%20
    Processing Record 205 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 206 of set3 | Unstoppable 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Unstoppable%20
    Processing Record 207 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 208 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 209 of set3 | Salt 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Salt%20
    Processing Record 210 of set3 | The Social Network 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Social%20Network%20
    Processing Record 211 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 212 of set3 | Alice in Wonderland 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Alice%20in%20Wonderland%20
    Processing Record 213 of set3 | Harry Potter and the Deathly Hallows Part 1 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Potter%20and%20the%20Deathly%20Hallows%20Part%201%20
    Processing Record 214 of set3 | Hereafter 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hereafter%20
    Processing Record 215 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 216 of set3 | Iron Man 2 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Iron%20Man%202%20
    Processing Record 217 of set3 | 127 Hours 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=127%20Hours%20
    Processing Record 218 of set3 | The Social Network 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Social%20Network%20
    Processing Record 219 of set3 | Toy Story 3 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Toy%20Story%203%20
    Processing Record 220 of set3 | True Grit 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=True%20Grit%20
    Processing Record 221 of set3 | Winter's Bone 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Winter's%20Bone%20
    Processing Record 222 of set3 | Another Year 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Another%20Year%20
    Processing Record 223 of set3 | The Fighter 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Fighter%20
    Processing Record 224 of set3 | Inception 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inception%20
    Processing Record 225 of set3 | The Kids Are All Right 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Kids%20Are%20All%20Right%20
    Processing Record 226 of set3 | The King's Speech 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20King's%20Speech%20
    Processing Record 227 of set3 | Kevin Brownlow
    <class 'IndexError'>
    list index out of range
    Processing Record 228 of set3 | Jean-Luc Godard
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jean-Luc%20Godard
    Processing Record 229 of set3 | Eli Wallach
    <class 'IndexError'>
    list index out of range
    Processing Record 230 of set3 | Francis Ford Coppola
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Francis%20Ford%20Coppola
    Processing Record 231 of set3 | Denny Clairmont
    <class 'IndexError'>
    list index out of range
    Processing Record 232 of set3 | Demián Bichir
    <class 'IndexError'>
    list index out of range
    Processing Record 233 of set3 | George Clooney
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=George%20Clooney
    Processing Record 234 of set3 | Jean Dujardin
    <class 'IndexError'>
    list index out of range
    Processing Record 235 of set3 | Gary Oldman
    <class 'IndexError'>
    list index out of range
    Processing Record 236 of set3 | Brad Pitt
    <class 'IndexError'>
    list index out of range
    Processing Record 237 of set3 | Kenneth Branagh
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Kenneth%20Branagh
    Processing Record 238 of set3 | Jonah Hill
    <class 'IndexError'>
    list index out of range
    Processing Record 239 of set3 | Nick Nolte
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nick%20Nolte
    Processing Record 240 of set3 | Christopher Plummer
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Christopher%20Plummer
    Processing Record 1 of set4 | Max von Sydow
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Max%20von%20Sydow
    Processing Record 2 of set4 | Glenn Close
    <class 'IndexError'>
    list index out of range
    Processing Record 3 of set4 | Viola Davis
    <class 'IndexError'>
    list index out of range
    Processing Record 4 of set4 | Rooney Mara
    <class 'IndexError'>
    list index out of range
    Processing Record 5 of set4 | Meryl Streep
    <class 'IndexError'>
    list index out of range
    Processing Record 6 of set4 | Michelle Williams
    <class 'IndexError'>
    list index out of range
    Processing Record 7 of set4 | Bérénice Bejo
    <class 'IndexError'>
    list index out of range
    Processing Record 8 of set4 | Jessica Chastain
    <class 'IndexError'>
    list index out of range
    Processing Record 9 of set4 | Melissa McCarthy
    <class 'IndexError'>
    list index out of range
    Processing Record 10 of set4 | Janet McTeer
    <class 'IndexError'>
    list index out of range
    Processing Record 11 of set4 | Octavia Spencer
    <class 'IndexError'>
    list index out of range
    Processing Record 12 of set4 | A Cat in Paris 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Cat%20in%20Paris%20
    Processing Record 13 of set4 | Chico & Rita 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Chico%20&%20Rita%20
    Processing Record 14 of set4 | Kung Fu Panda 2 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Kung%20Fu%20Panda%202%20
    Processing Record 15 of set4 | Puss in Boots 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Puss%20in%20Boots%20
    Processing Record 16 of set4 | Rango 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Rango%20
    Processing Record 17 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 18 of set4 | Harry Potter and the Deathly Hallows Part 2 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Potter%20and%20the%20Deathly%20Hallows%20Part%202%20
    Processing Record 19 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 20 of set4 | Midnight in Paris 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Midnight%20in%20Paris%20
    Processing Record 21 of set4 | War Horse 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20Horse%20
    Processing Record 22 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 23 of set4 | The Girl with the Dragon Tattoo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Girl%20with%20the%20Dragon%20Tattoo%20
    Processing Record 24 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 25 of set4 | The Tree of Life 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Tree%20of%20Life%20
    Processing Record 26 of set4 | War Horse 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20Horse%20
    Processing Record 27 of set4 | Anonymous 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anonymous%20
    Processing Record 28 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 29 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 30 of set4 | Jane Eyre 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jane%20Eyre%20
    Processing Record 31 of set4 | W.E. 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=W.E.%20
    Processing Record 32 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 33 of set4 | The Descendants 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Descendants%20
    Processing Record 34 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 35 of set4 | Midnight in Paris 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Midnight%20in%20Paris%20
    Processing Record 36 of set4 | The Tree of Life 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Tree%20of%20Life%20
    Processing Record 37 of set4 | Hell and Back Again 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hell%20and%20Back%20Again%20
    Processing Record 38 of set4 | If a Tree Falls: A Story of the Earth Liberation Front 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=If%20a%20Tree%20Falls:%20A%20Story%20of%20the%20Earth%20Liberation%20Front%20
    Processing Record 39 of set4 | Paradise Lost 3: Purgatory 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Paradise%20Lost%203:%20Purgatory%20
    Processing Record 40 of set4 | Pina 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pina%20
    Processing Record 41 of set4 | Undefeated 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Undefeated%20
    Processing Record 42 of set4 | The Barber of Birmingham: Foot Soldier of the Civil Rights Movement 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Barber%20of%20Birmingham:%20Foot%20Soldier%20of%20the%20Civil%20Rights%20Movement%20
    Processing Record 43 of set4 | God Is the Bigger Elvis 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=God%20Is%20the%20Bigger%20Elvis%20
    Processing Record 44 of set4 | Incident in New Baghdad 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Incident%20in%20New%20Baghdad%20
    Processing Record 45 of set4 | Saving Face 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Saving%20Face%20
    Processing Record 46 of set4 | The Tsunami and the Cherry Blossom 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Tsunami%20and%20the%20Cherry%20Blossom%20
    Processing Record 47 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 48 of set4 | The Descendants 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Descendants%20
    Processing Record 49 of set4 | The Girl with the Dragon Tattoo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Girl%20with%20the%20Dragon%20Tattoo%20
    Processing Record 50 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 51 of set4 | Moneyball 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Moneyball%20
    Processing Record 52 of set4 | Bullhead 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bullhead%20
    Processing Record 53 of set4 | Footnote 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Footnote%20
    Processing Record 54 of set4 | In Darkness 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=In%20Darkness%20
    Processing Record 55 of set4 | Monsieur Lazhar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Monsieur%20Lazhar%20
    Processing Record 56 of set4 | A Separation 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Separation%20
    Processing Record 57 of set4 | Albert Nobbs 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Albert%20Nobbs%20
    Processing Record 58 of set4 | Harry Potter and the Deathly Hallows Part 2 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Potter%20and%20the%20Deathly%20Hallows%20Part%202%20
    Processing Record 59 of set4 | The Iron Lady 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Iron%20Lady%20
    Processing Record 60 of set4 | The Adventures of Tintin 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Adventures%20of%20Tintin%20
    Processing Record 61 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 62 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 63 of set4 | Tinker Tailor Soldier Spy 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tinker%20Tailor%20Soldier%20Spy%20
    Processing Record 64 of set4 | War Horse 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20Horse%20
    Processing Record 65 of set4 | "Man Or Muppet" from The Muppets
    <class 'IndexError'>
    list index out of range
    Processing Record 66 of set4 | "Real In Rio" from Rio
    <class 'IndexError'>
    list index out of range
    Processing Record 67 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 68 of set4 | The Descendants 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Descendants%20
    Processing Record 69 of set4 | Extremely Loud & Incredibly Close 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Extremely%20Loud%20&%20Incredibly%20Close%20
    Processing Record 70 of set4 | The Help 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Help%20
    Processing Record 71 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 72 of set4 | Midnight in Paris 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Midnight%20in%20Paris%20
    Processing Record 73 of set4 | Moneyball 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Moneyball%20
    Processing Record 74 of set4 | The Tree of Life 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Tree%20of%20Life%20
    Processing Record 75 of set4 | War Horse 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20Horse%20
    Processing Record 76 of set4 | Dimanche/Sunday 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dimanche/Sunday%20
    Processing Record 77 of set4 | The Fantastic Flying Books of Mr. Morris Lessmore 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Fantastic%20Flying%20Books%20of%20Mr.%20Morris%20Lessmore%20
    Processing Record 78 of set4 | La Luna 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=La%20Luna%20
    Processing Record 79 of set4 | A Morning Stroll 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Morning%20Stroll%20
    Processing Record 80 of set4 | Wild Life 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Wild%20Life%20
    Processing Record 81 of set4 | Pentecost 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Pentecost%20
    Processing Record 82 of set4 | Raju 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Raju%20
    Processing Record 83 of set4 | The Shore 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Shore%20
    Processing Record 84 of set4 | Time Freak 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Time%20Freak%20
    Processing Record 85 of set4 | Tuba Atlantic 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tuba%20Atlantic%20
    Processing Record 86 of set4 | Drive 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Drive%20
    Processing Record 87 of set4 | The Girl with the Dragon Tattoo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Girl%20with%20the%20Dragon%20Tattoo%20
    Processing Record 88 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 89 of set4 | Transformers: Dark of the Moon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Transformers:%20Dark%20of%20the%20Moon%20
    Processing Record 90 of set4 | War Horse 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20Horse%20
    Processing Record 91 of set4 | The Girl with the Dragon Tattoo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Girl%20with%20the%20Dragon%20Tattoo%20
    Processing Record 92 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 93 of set4 | Moneyball 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Moneyball%20
    Processing Record 94 of set4 | Transformers: Dark of the Moon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Transformers:%20Dark%20of%20the%20Moon%20
    Processing Record 95 of set4 | War Horse 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20Horse%20
    Processing Record 96 of set4 | Harry Potter and the Deathly Hallows Part 2 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Potter%20and%20the%20Deathly%20Hallows%20Part%202%20
    Processing Record 97 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 98 of set4 | Real Steel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Real%20Steel%20
    Processing Record 99 of set4 | Rise of the Planet of the Apes 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Rise%20of%20the%20Planet%20of%20the%20Apes%20
    Processing Record 100 of set4 | Transformers: Dark of the Moon 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Transformers:%20Dark%20of%20the%20Moon%20
    Processing Record 101 of set4 | The Descendants 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Descendants%20
    Processing Record 102 of set4 | Hugo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugo%20
    Processing Record 103 of set4 | The Ides of March 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Ides%20of%20March%20
    Processing Record 104 of set4 | Moneyball 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Moneyball%20
    Processing Record 105 of set4 | Tinker Tailor Soldier Spy 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tinker%20Tailor%20Soldier%20Spy%20
    Processing Record 106 of set4 | The Artist 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Artist%20
    Processing Record 107 of set4 | Bridesmaids 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bridesmaids%20
    Processing Record 108 of set4 | Margin Call 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Margin%20Call%20
    Processing Record 109 of set4 | Midnight in Paris 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Midnight%20in%20Paris%20
    Processing Record 110 of set4 | A Separation 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Separation%20
    Processing Record 111 of set4 | Oprah Winfrey
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Oprah%20Winfrey
    Processing Record 112 of set4 | James Earl Jones.
    <class 'IndexError'>
    list index out of range
    Processing Record 113 of set4 | Dick Smith
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dick%20Smith
    Processing Record 114 of set4 | Douglas Trumbull
    <class 'IndexError'>
    list index out of range
    Processing Record 115 of set4 | Jonathan Erland
    <class 'IndexError'>
    list index out of range
    Processing Record 116 of set4 | Bradley Cooper
    <class 'IndexError'>
    list index out of range
    Processing Record 117 of set4 | Daniel Day-Lewis
    <class 'IndexError'>
    list index out of range
    Processing Record 118 of set4 | Hugh Jackman
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hugh%20Jackman
    Processing Record 119 of set4 | Joaquin Phoenix
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Joaquin%20Phoenix
    Processing Record 120 of set4 | Denzel Washington
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Denzel%20Washington
    Processing Record 121 of set4 | Alan Arkin
    <class 'IndexError'>
    list index out of range
    Processing Record 122 of set4 | Robert De Niro
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Robert%20De%20Niro
    Processing Record 123 of set4 | Philip Seymour Hoffman
    <class 'IndexError'>
    list index out of range
    Processing Record 124 of set4 | Tommy Lee Jones
    <class 'IndexError'>
    list index out of range
    Processing Record 125 of set4 | Christoph Waltz
    <class 'IndexError'>
    list index out of range
    Processing Record 126 of set4 | Jessica Chastain
    <class 'IndexError'>
    list index out of range
    Processing Record 127 of set4 | Jennifer Lawrence
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jennifer%20Lawrence
    Processing Record 128 of set4 | Emmanuelle Riva
    <class 'IndexError'>
    list index out of range
    Processing Record 129 of set4 | Quvenzhané Wallis
    <class 'IndexError'>
    list index out of range
    Processing Record 130 of set4 | Naomi Watts
    <class 'IndexError'>
    list index out of range
    Processing Record 131 of set4 | Amy Adams
    <class 'IndexError'>
    list index out of range
    Processing Record 132 of set4 | Sally Field
    <class 'IndexError'>
    list index out of range
    Processing Record 133 of set4 | Anne Hathaway
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anne%20Hathaway
    Processing Record 134 of set4 | Helen Hunt
    <class 'IndexError'>
    list index out of range
    Processing Record 135 of set4 | Jacki Weaver
    <class 'IndexError'>
    list index out of range
    Processing Record 136 of set4 | Brave 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brave%20
    Processing Record 137 of set4 | Frankenweenie 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Frankenweenie%20
    Processing Record 138 of set4 | ParaNorman 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=ParaNorman%20
    Processing Record 139 of set4 | The Pirates! Band of Misfits 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Pirates!%20Band%20of%20Misfits%20
    Processing Record 140 of set4 | Wreck-It Ralph 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Wreck-It%20Ralph%20
    Processing Record 141 of set4 | Anna Karenina 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anna%20Karenina%20
    Processing Record 142 of set4 | Django Unchained 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Django%20Unchained%20
    Processing Record 143 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 144 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 145 of set4 | Skyfall 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Skyfall%20
    Processing Record 146 of set4 | Anna Karenina 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anna%20Karenina%20
    Processing Record 147 of set4 | Les Misérables 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Les%20Mis%C3%A9rables%20
    Processing Record 148 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 149 of set4 | Mirror Mirror 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mirror%20Mirror%20
    Processing Record 150 of set4 | Snow White and the Huntsman 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Snow%20White%20and%20the%20Huntsman%20
    Processing Record 151 of set4 | Amour 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Amour%20
    Processing Record 152 of set4 | Beasts of the Southern Wild 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Beasts%20of%20the%20Southern%20Wild%20
    Processing Record 153 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 154 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 155 of set4 | Silver Linings Playbook 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Silver%20Linings%20Playbook%20
    Processing Record 156 of set4 | 5 Broken Cameras 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=5%20Broken%20Cameras%20
    Processing Record 157 of set4 | The Gatekeepers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Gatekeepers%20
    Processing Record 158 of set4 | How to Survive a Plague 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=How%20to%20Survive%20a%20Plague%20
    Processing Record 159 of set4 | The Invisible War 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Invisible%20War%20
    Processing Record 160 of set4 | Searching for Sugar Man 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Searching%20for%20Sugar%20Man%20
    Processing Record 161 of set4 | Inocente 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inocente%20
    Processing Record 162 of set4 | Kings Point 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Kings%20Point%20
    Processing Record 163 of set4 | Mondays at Racine 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mondays%20at%20Racine%20
    Processing Record 164 of set4 | Open Heart 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Open%20Heart%20
    Processing Record 165 of set4 | Redemption 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Redemption%20
    Processing Record 166 of set4 | Argo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Argo%20
    Processing Record 167 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 168 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 169 of set4 | Silver Linings Playbook 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Silver%20Linings%20Playbook%20
    Processing Record 170 of set4 | Zero Dark Thirty 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Zero%20Dark%20Thirty%20
    Processing Record 171 of set4 | Amour 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Amour%20
    Processing Record 172 of set4 | Kon-Tiki 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Kon-Tiki%20
    Processing Record 173 of set4 | No 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=No%20
    Processing Record 174 of set4 | A Royal Affair 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Royal%20Affair%20
    Processing Record 175 of set4 | War Witch 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=War%20Witch%20
    Processing Record 176 of set4 | Hitchcock 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hitchcock%20
    Processing Record 177 of set4 | The Hobbit: An Unexpected Journey 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hobbit:%20An%20Unexpected%20Journey%20
    Processing Record 178 of set4 | Les Misérables 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Les%20Mis%C3%A9rables%20
    Processing Record 179 of set4 | Anna Karenina 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anna%20Karenina%20
    Processing Record 180 of set4 | Argo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Argo%20
    Processing Record 181 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 182 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 183 of set4 | Skyfall 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Skyfall%20
    Processing Record 184 of set4 | "Before My Time" from Chasing Ice
    <class 'IndexError'>
    list index out of range
    Processing Record 185 of set4 | "Everybody Needs A Best Friend" from Ted
    <class 'IndexError'>
    list index out of range
    Processing Record 186 of set4 | "Pi's Lullaby" from Life of Pi
    <class 'IndexError'>
    list index out of range
    Processing Record 187 of set4 | "Skyfall" from Skyfall
    <class 'IndexError'>
    list index out of range
    Processing Record 188 of set4 | "Suddenly" from Les Misérables
    <class 'IndexError'>
    list index out of range
    Processing Record 189 of set4 | Amour 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Amour%20
    Processing Record 190 of set4 | Argo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Argo%20
    Processing Record 191 of set4 | Beasts of the Southern Wild 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Beasts%20of%20the%20Southern%20Wild%20
    Processing Record 192 of set4 | Django Unchained 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Django%20Unchained%20
    Processing Record 193 of set4 | Les Misérables 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Les%20Mis%C3%A9rables%20
    Processing Record 194 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 195 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 196 of set4 | Silver Linings Playbook 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Silver%20Linings%20Playbook%20
    Processing Record 197 of set4 | Zero Dark Thirty 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Zero%20Dark%20Thirty%20
    Processing Record 198 of set4 | Anna Karenina 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anna%20Karenina%20
    Processing Record 199 of set4 | The Hobbit: An Unexpected Journey 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hobbit:%20An%20Unexpected%20Journey%20
    Processing Record 200 of set4 | Les Misérables 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Les%20Mis%C3%A9rables%20
    Processing Record 201 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 202 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 203 of set4 | Adam and Dog 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Adam%20and%20Dog%20
    Processing Record 204 of set4 | Fresh Guacamole 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Fresh%20Guacamole%20
    Processing Record 205 of set4 | Head over Heels 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Head%20over%20Heels%20
    Processing Record 206 of set4 | Maggie Simpson in "The Longest Daycare" 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Maggie%20Simpson%20in%20%22The%20Longest%20Daycare%22%20
    Processing Record 207 of set4 | Paperman 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Paperman%20
    Processing Record 208 of set4 | Asad 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Asad%20
    Processing Record 209 of set4 | Buzkashi Boys 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Buzkashi%20Boys%20
    Processing Record 210 of set4 | Curfew 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Curfew%20
    Processing Record 211 of set4 | Death of a Shadow (Dood van een Schaduw) 
    <class 'IndexError'>
    list index out of range
    Processing Record 212 of set4 | Henry 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Henry%20
    Processing Record 213 of set4 | Argo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Argo%20
    Processing Record 214 of set4 | Django Unchained 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Django%20Unchained%20
    Processing Record 215 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 216 of set4 | Skyfall 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Skyfall%20
    Processing Record 217 of set4 | Zero Dark Thirty 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Zero%20Dark%20Thirty%20
    Processing Record 218 of set4 | Argo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Argo%20
    Processing Record 219 of set4 | Les Misérables 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Les%20Mis%C3%A9rables%20
    Processing Record 220 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 221 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 222 of set4 | Skyfall 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Skyfall%20
    Processing Record 223 of set4 | The Hobbit: An Unexpected Journey 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hobbit:%20An%20Unexpected%20Journey%20
    Processing Record 224 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 225 of set4 | Marvel's The Avengers 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Marvel's%20The%20Avengers%20
    Processing Record 226 of set4 | Prometheus 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Prometheus%20
    Processing Record 227 of set4 | Snow White and the Huntsman 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Snow%20White%20and%20the%20Huntsman%20
    Processing Record 228 of set4 | Argo 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Argo%20
    Processing Record 229 of set4 | Beasts of the Southern Wild 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Beasts%20of%20the%20Southern%20Wild%20
    Processing Record 230 of set4 | Life of Pi 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Life%20of%20Pi%20
    Processing Record 231 of set4 | Lincoln 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lincoln%20
    Processing Record 232 of set4 | Silver Linings Playbook 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Silver%20Linings%20Playbook%20
    Processing Record 233 of set4 | Amour 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Amour%20
    Processing Record 234 of set4 | Django Unchained 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Django%20Unchained%20
    Processing Record 235 of set4 | Flight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Flight%20
    Processing Record 236 of set4 | Moonrise Kingdom 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Moonrise%20Kingdom%20
    Processing Record 237 of set4 | Zero Dark Thirty 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Zero%20Dark%20Thirty%20
    Processing Record 238 of set4 | Jeffrey Katzenberg
    <class 'IndexError'>
    list index out of range
    Processing Record 239 of set4 | Hal Needham
    <class 'IndexError'>
    list index out of range
    Processing Record 240 of set4 | D.A. Pennebaker
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=D.A.%20Pennebaker
    Processing Record 1 of set5 | George Stevens, Jr.
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=George%20Stevens,%20Jr.
    Processing Record 2 of set5 | Bill Taylor
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bill%20Taylor
    Processing Record 3 of set5 | Christian Bale
    <class 'IndexError'>
    list index out of range
    Processing Record 4 of set5 | Bruce Dern
    <class 'IndexError'>
    list index out of range
    Processing Record 5 of set5 | Leonardo DiCaprio
    <class 'IndexError'>
    list index out of range
    Processing Record 6 of set5 | Chiwetel Ejiofor
    <class 'IndexError'>
    list index out of range
    Processing Record 7 of set5 | Matthew McConaughey
    <class 'IndexError'>
    list index out of range
    Processing Record 8 of set5 | Barkhad Abdi
    <class 'IndexError'>
    list index out of range
    Processing Record 9 of set5 | Bradley Cooper
    <class 'IndexError'>
    list index out of range
    Processing Record 10 of set5 | Michael Fassbender
    <class 'IndexError'>
    list index out of range
    Processing Record 11 of set5 | Jonah Hill
    <class 'IndexError'>
    list index out of range
    Processing Record 12 of set5 | Jared Leto
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jared%20Leto
    Processing Record 13 of set5 | Amy Adams
    <class 'IndexError'>
    list index out of range
    Processing Record 14 of set5 | Cate Blanchett
    <class 'IndexError'>
    list index out of range
    Processing Record 15 of set5 | Sandra Bullock
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sandra%20Bullock
    Processing Record 16 of set5 | Judi Dench
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Judi%20Dench
    Processing Record 17 of set5 | Meryl Streep
    <class 'IndexError'>
    list index out of range
    Processing Record 18 of set5 | Sally Hawkins
    <class 'IndexError'>
    list index out of range
    Processing Record 19 of set5 | Jennifer Lawrence
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jennifer%20Lawrence
    Processing Record 20 of set5 | Lupita Nyong'o
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lupita%20Nyong'o
    Processing Record 21 of set5 | Julia Roberts
    <class 'IndexError'>
    list index out of range
    Processing Record 22 of set5 | June Squibb
    <class 'IndexError'>
    list index out of range
    Processing Record 23 of set5 | The Croods 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Croods%20
    Processing Record 24 of set5 | Despicable Me 2 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Despicable%20Me%202%20
    Processing Record 25 of set5 | Ernest & Celestine 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ernest%20&%20Celestine%20
    Processing Record 26 of set5 | Frozen 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Frozen%20
    Processing Record 27 of set5 | The Wind Rises 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Wind%20Rises%20
    Processing Record 28 of set5 | The Grandmaster 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grandmaster%20
    Processing Record 29 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 30 of set5 | Inside Llewyn Davis 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inside%20Llewyn%20Davis%20
    Processing Record 31 of set5 | Nebraska 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nebraska%20
    Processing Record 32 of set5 | Prisoners 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Prisoners%20
    Processing Record 33 of set5 | American Hustle 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Hustle%20
    Processing Record 34 of set5 | The Grandmaster 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grandmaster%20
    Processing Record 35 of set5 | The Great Gatsby 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Great%20Gatsby%20
    Processing Record 36 of set5 | The Invisible Woman 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Invisible%20Woman%20
    Processing Record 37 of set5 | 12 Years a Slave 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=12%20Years%20a%20Slave%20
    Processing Record 38 of set5 | American Hustle 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Hustle%20
    Processing Record 39 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 40 of set5 | Nebraska 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nebraska%20
    Processing Record 41 of set5 | 12 Years a Slave 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=12%20Years%20a%20Slave%20
    Processing Record 42 of set5 | The Wolf of Wall Street 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Wolf%20of%20Wall%20Street%20
    Processing Record 43 of set5 | The Act of Killing 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Act%20of%20Killing%20
    Processing Record 44 of set5 | Cutie and the Boxer 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Cutie%20and%20the%20Boxer%20
    Processing Record 45 of set5 | Dirty Wars 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dirty%20Wars%20
    Processing Record 46 of set5 | The Square 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Square%20
    Processing Record 47 of set5 | 20 Feet from Stardom 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=20%20Feet%20from%20Stardom%20
    Processing Record 48 of set5 | CaveDigger 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=CaveDigger%20
    Processing Record 49 of set5 | Facing Fear 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Facing%20Fear%20
    Processing Record 50 of set5 | Karama Has No Walls 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Karama%20Has%20No%20Walls%20
    Processing Record 51 of set5 | The Lady in Number 6: Music Saved My Life 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Lady%20in%20Number%206:%20Music%20Saved%20My%20Life%20
    Processing Record 52 of set5 | Prison Terminal: The Last Days of Private Jack Hall 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Prison%20Terminal:%20The%20Last%20Days%20of%20Private%20Jack%20Hall%20
    Processing Record 53 of set5 | American Hustle 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Hustle%20
    Processing Record 54 of set5 | Captain Phillips 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Captain%20Phillips%20
    Processing Record 55 of set5 | Dallas Buyers Club 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dallas%20Buyers%20Club%20
    Processing Record 56 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 57 of set5 | 12 Years a Slave 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=12%20Years%20a%20Slave%20
    Processing Record 58 of set5 | The Broken Circle Breakdown 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Broken%20Circle%20Breakdown%20
    Processing Record 59 of set5 | The Great Beauty 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Great%20Beauty%20
    Processing Record 60 of set5 | The Hunt 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hunt%20
    Processing Record 61 of set5 | The Missing Picture 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Missing%20Picture%20
    Processing Record 62 of set5 | Omar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Omar%20
    Processing Record 63 of set5 | Dallas Buyers Club 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dallas%20Buyers%20Club%20
    Processing Record 64 of set5 | Jackass Presents: Bad Grandpa 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jackass%20Presents:%20Bad%20Grandpa%20
    Processing Record 65 of set5 | The Lone Ranger 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Lone%20Ranger%20
    Processing Record 66 of set5 | The Book Thief 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Book%20Thief%20
    Processing Record 67 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 68 of set5 | Her 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Her%20
    Processing Record 69 of set5 | Philomena 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Philomena%20
    Processing Record 70 of set5 | Saving Mr. Banks 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Saving%20Mr.%20Banks%20
    Processing Record 71 of set5 | "Alone Yet Not Alone" from Alone Yet Not Alone
    <class 'IndexError'>
    list index out of range
    Processing Record 72 of set5 | "Happy" from Despicable Me 2
    <class 'IndexError'>
    list index out of range
    Processing Record 73 of set5 | "Let It Go" from Frozen
    <class 'IndexError'>
    list index out of range
    Processing Record 74 of set5 | "The Moon Song" from Her
    <class 'IndexError'>
    list index out of range
    Processing Record 75 of set5 | "Ordinary Love" from Mandela: Long Walk to Freedom
    <class 'IndexError'>
    list index out of range
    Processing Record 76 of set5 | American Hustle 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Hustle%20
    Processing Record 77 of set5 | Captain Phillips 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Captain%20Phillips%20
    Processing Record 78 of set5 | Dallas Buyers Club 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dallas%20Buyers%20Club%20
    Processing Record 79 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 80 of set5 | Her 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Her%20
    Processing Record 81 of set5 | Nebraska 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nebraska%20
    Processing Record 82 of set5 | Philomena 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Philomena%20
    Processing Record 83 of set5 | 12 Years a Slave 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=12%20Years%20a%20Slave%20
    Processing Record 84 of set5 | The Wolf of Wall Street 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Wolf%20of%20Wall%20Street%20
    Processing Record 85 of set5 | American Hustle 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Hustle%20
    Processing Record 86 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 87 of set5 | The Great Gatsby 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Great%20Gatsby%20
    Processing Record 88 of set5 | Her 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Her%20
    Processing Record 89 of set5 | 12 Years a Slave 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=12%20Years%20a%20Slave%20
    Processing Record 90 of set5 | Feral 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Feral%20
    Processing Record 91 of set5 | Get a Horse! 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Get%20a%20Horse!%20
    Processing Record 92 of set5 | Mr. Hublot 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mr.%20Hublot%20
    Processing Record 93 of set5 | Possessions 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Possessions%20
    Processing Record 94 of set5 | Room on the Broom 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Room%20on%20the%20Broom%20
    Processing Record 95 of set5 | Aquel No Era Yo (That Wasn't Me) 
    <class 'IndexError'>
    list index out of range
    Processing Record 96 of set5 | Avant Que De Tout Perdre (Just before Losing Everything) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Avant%20Que%20De%20Tout%20Perdre%20(Just%20before%20Losing%20Everything)%20
    Processing Record 97 of set5 | Helium 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Helium%20
    Processing Record 98 of set5 | Pitääkö Mun Kaikki Hoitaa? (Do I Have to Take Care of Everything?) 
    <class 'IndexError'>
    list index out of range
    Processing Record 99 of set5 | The Voorman Problem 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Voorman%20Problem%20
    Processing Record 100 of set5 | All Is Lost 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=All%20Is%20Lost%20
    Processing Record 101 of set5 | Captain Phillips 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Captain%20Phillips%20
    Processing Record 102 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 103 of set5 | The Hobbit: The Desolation of Smaug 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hobbit:%20The%20Desolation%20of%20Smaug%20
    Processing Record 104 of set5 | Lone Survivor 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lone%20Survivor%20
    Processing Record 105 of set5 | Captain Phillips 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Captain%20Phillips%20
    Processing Record 106 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 107 of set5 | The Hobbit: The Desolation of Smaug 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hobbit:%20The%20Desolation%20of%20Smaug%20
    Processing Record 108 of set5 | Inside Llewyn Davis 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inside%20Llewyn%20Davis%20
    Processing Record 109 of set5 | Lone Survivor 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Lone%20Survivor%20
    Processing Record 110 of set5 | Gravity 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Gravity%20
    Processing Record 111 of set5 | The Hobbit: The Desolation of Smaug 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hobbit:%20The%20Desolation%20of%20Smaug%20
    Processing Record 112 of set5 | Iron Man 3 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Iron%20Man%203%20
    Processing Record 113 of set5 | The Lone Ranger 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Lone%20Ranger%20
    Processing Record 114 of set5 | Star Trek Into Darkness 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Trek%20Into%20Darkness%20
    Processing Record 115 of set5 | Before Midnight 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Before%20Midnight%20
    Processing Record 116 of set5 | Captain Phillips 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Captain%20Phillips%20
    Processing Record 117 of set5 | Philomena 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Philomena%20
    Processing Record 118 of set5 | 12 Years a Slave 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=12%20Years%20a%20Slave%20
    Processing Record 119 of set5 | The Wolf of Wall Street 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Wolf%20of%20Wall%20Street%20
    Processing Record 120 of set5 | American Hustle 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Hustle%20
    Processing Record 121 of set5 | Blue Jasmine 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Blue%20Jasmine%20
    Processing Record 122 of set5 | Dallas Buyers Club 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dallas%20Buyers%20Club%20
    Processing Record 123 of set5 | Her 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Her%20
    Processing Record 124 of set5 | Nebraska 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nebraska%20
    Processing Record 125 of set5 | Angelina Jolie
    <class 'IndexError'>
    list index out of range
    Processing Record 126 of set5 | Angela Lansbury
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Angela%20Lansbury
    Processing Record 127 of set5 | Steve Martin
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Steve%20Martin
    Processing Record 128 of set5 | Piero Tosi
    <class 'IndexError'>
    list index out of range
    Processing Record 129 of set5 | Peter W. Anderson
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Peter%20W.%20Anderson
    Processing Record 130 of set5 | Charles "Tad" Marburg
    <class 'IndexError'>
    list index out of range
    Processing Record 131 of set5 | Steve Carell
    <class 'IndexError'>
    list index out of range
    Processing Record 132 of set5 | Bradley Cooper
    <class 'IndexError'>
    list index out of range
    Processing Record 133 of set5 | Benedict Cumberbatch
    <class 'IndexError'>
    list index out of range
    Processing Record 134 of set5 | Michael Keaton
    <class 'IndexError'>
    list index out of range
    Processing Record 135 of set5 | Eddie Redmayne
    <class 'IndexError'>
    list index out of range
    Processing Record 136 of set5 | Robert Duvall
    <class 'IndexError'>
    list index out of range
    Processing Record 137 of set5 | Ethan Hawke
    <class 'IndexError'>
    list index out of range
    Processing Record 138 of set5 | Edward Norton
    <class 'IndexError'>
    list index out of range
    Processing Record 139 of set5 | Mark Ruffalo
    <class 'IndexError'>
    list index out of range
    Processing Record 140 of set5 | J.K. Simmons
    <class 'IndexError'>
    list index out of range
    Processing Record 141 of set5 | Marion Cotillard
    <class 'IndexError'>
    list index out of range
    Processing Record 142 of set5 | Felicity Jones
    <class 'IndexError'>
    list index out of range
    Processing Record 143 of set5 | Julianne Moore
    <class 'IndexError'>
    list index out of range
    Processing Record 144 of set5 | Rosamund Pike
    <class 'IndexError'>
    list index out of range
    Processing Record 145 of set5 | Reese Witherspoon
    <class 'IndexError'>
    list index out of range
    Processing Record 146 of set5 | Patricia Arquette
    <class 'IndexError'>
    list index out of range
    Processing Record 147 of set5 | Laura Dern
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Laura%20Dern
    Processing Record 148 of set5 | Keira Knightley
    <class 'IndexError'>
    list index out of range
    Processing Record 149 of set5 | Emma Stone
    <class 'IndexError'>
    list index out of range
    Processing Record 150 of set5 | Meryl Streep
    <class 'IndexError'>
    list index out of range
    Processing Record 151 of set5 | Big Hero 6 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Big%20Hero%206%20
    Processing Record 152 of set5 | The Boxtrolls 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Boxtrolls%20
    Processing Record 153 of set5 | How to Train Your Dragon 2 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=How%20to%20Train%20Your%20Dragon%202%20
    Processing Record 154 of set5 | Song of the Sea 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Song%20of%20the%20Sea%20
    Processing Record 155 of set5 | The Tale of the Princess Kaguya 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Tale%20of%20the%20Princess%20Kaguya%20
    Processing Record 156 of set5 | Birdman or (The Unexpected Virtue of Ignorance) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Birdman%20or%20(The%20Unexpected%20Virtue%20of%20Ignorance)%20
    Processing Record 157 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 158 of set5 | Ida 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ida%20
    Processing Record 159 of set5 | Mr. Turner 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mr.%20Turner%20
    Processing Record 160 of set5 | Unbroken 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Unbroken%20
    Processing Record 161 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 162 of set5 | Inherent Vice 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inherent%20Vice%20
    Processing Record 163 of set5 | Into the Woods 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Into%20the%20Woods%20
    Processing Record 164 of set5 | Maleficent 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Maleficent%20
    Processing Record 165 of set5 | Mr. Turner 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mr.%20Turner%20
    Processing Record 166 of set5 | Birdman or (The Unexpected Virtue of Ignorance) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Birdman%20or%20(The%20Unexpected%20Virtue%20of%20Ignorance)%20
    Processing Record 167 of set5 | Boyhood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Boyhood%20
    Processing Record 168 of set5 | Foxcatcher 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Foxcatcher%20
    Processing Record 169 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 170 of set5 | The Imitation Game 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imitation%20Game%20
    Processing Record 171 of set5 | CitizenFour 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=CitizenFour%20
    Processing Record 172 of set5 | Finding Vivian Maier 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Finding%20Vivian%20Maier%20
    Processing Record 173 of set5 | Last Days in Vietnam 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Last%20Days%20in%20Vietnam%20
    Processing Record 174 of set5 | The Salt of the Earth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Salt%20of%20the%20Earth%20
    Processing Record 175 of set5 | Virunga 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Virunga%20
    Processing Record 176 of set5 | Crisis Hotline: Veterans Press 1 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Crisis%20Hotline:%20Veterans%20Press%201%20
    Processing Record 177 of set5 | Joanna 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Joanna%20
    Processing Record 178 of set5 | Our Curse 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Our%20Curse%20
    Processing Record 179 of set5 | The Reaper (La Parka) 
    <class 'IndexError'>
    list index out of range
    Processing Record 180 of set5 | White Earth 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=White%20Earth%20
    Processing Record 181 of set5 | American Sniper 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Sniper%20
    Processing Record 182 of set5 | Boyhood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Boyhood%20
    Processing Record 183 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 184 of set5 | The Imitation Game 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imitation%20Game%20
    Processing Record 185 of set5 | Whiplash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Whiplash%20
    Processing Record 186 of set5 | Ida 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ida%20
    Processing Record 187 of set5 | Leviathan 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Leviathan%20
    Processing Record 188 of set5 | Tangerines 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tangerines%20
    Processing Record 189 of set5 | Timbuktu 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Timbuktu%20
    Processing Record 190 of set5 | Wild Tales 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Wild%20Tales%20
    Processing Record 191 of set5 | Foxcatcher 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Foxcatcher%20
    Processing Record 192 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 193 of set5 | Guardians of the Galaxy 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Guardians%20of%20the%20Galaxy%20
    Processing Record 194 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 195 of set5 | The Imitation Game 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imitation%20Game%20
    Processing Record 196 of set5 | Interstellar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Interstellar%20
    Processing Record 197 of set5 | Mr. Turner 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mr.%20Turner%20
    Processing Record 198 of set5 | The Theory of Everything 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Theory%20of%20Everything%20
    Processing Record 199 of set5 | "Everything Is Awesome" from The Lego Movie
    <class 'IndexError'>
    list index out of range
    Processing Record 200 of set5 | "Glory" from Selma
    <class 'IndexError'>
    list index out of range
    Processing Record 201 of set5 | "Grateful" from Beyond the Lights
    <class 'IndexError'>
    list index out of range
    Processing Record 202 of set5 | "I'm Not Gonna Miss You" from Glen Campbell...I'll Be Me
    <class 'IndexError'>
    list index out of range
    Processing Record 203 of set5 | "Lost Stars" from Begin Again
    <class 'IndexError'>
    list index out of range
    Processing Record 204 of set5 | American Sniper 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Sniper%20
    Processing Record 205 of set5 | Birdman or (The Unexpected Virtue of Ignorance) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Birdman%20or%20(The%20Unexpected%20Virtue%20of%20Ignorance)%20
    Processing Record 206 of set5 | Boyhood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Boyhood%20
    Processing Record 207 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 208 of set5 | The Imitation Game 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imitation%20Game%20
    Processing Record 209 of set5 | Selma 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Selma%20
    Processing Record 210 of set5 | The Theory of Everything 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Theory%20of%20Everything%20
    Processing Record 211 of set5 | Whiplash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Whiplash%20
    Processing Record 212 of set5 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 213 of set5 | The Imitation Game 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imitation%20Game%20
    Processing Record 214 of set5 | Interstellar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Interstellar%20
    Processing Record 215 of set5 | Into the Woods 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Into%20the%20Woods%20
    Processing Record 216 of set5 | Mr. Turner 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mr.%20Turner%20
    Processing Record 217 of set5 | The Bigger Picture 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Bigger%20Picture%20
    Processing Record 218 of set5 | The Dam Keeper 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Dam%20Keeper%20
    Processing Record 219 of set5 | Feast 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Feast%20
    Processing Record 220 of set5 | Me and My Moulton 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Me%20and%20My%20Moulton%20
    Processing Record 221 of set5 | A Single Life 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Single%20Life%20
    Processing Record 222 of set5 | Aya 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Aya%20
    Processing Record 223 of set5 | Boogaloo and Graham 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Boogaloo%20and%20Graham%20
    Processing Record 224 of set5 | Butter Lamp (La Lampe Au Beurre De Yak) 
    <class 'IndexError'>
    list index out of range
    Processing Record 225 of set5 | Parvaneh 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Parvaneh%20
    Processing Record 226 of set5 | The Phone Call 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Phone%20Call%20
    Processing Record 227 of set5 | American Sniper 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Sniper%20
    Processing Record 228 of set5 | Birdman or (The Unexpected Virtue of Ignorance) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Birdman%20or%20(The%20Unexpected%20Virtue%20of%20Ignorance)%20
    Processing Record 229 of set5 | The Hobbit: The Battle of the Five Armies 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hobbit:%20The%20Battle%20of%20the%20Five%20Armies%20
    Processing Record 230 of set5 | Interstellar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Interstellar%20
    Processing Record 231 of set5 | Unbroken 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Unbroken%20
    Processing Record 232 of set5 | American Sniper 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Sniper%20
    Processing Record 233 of set5 | Birdman or (The Unexpected Virtue of Ignorance) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Birdman%20or%20(The%20Unexpected%20Virtue%20of%20Ignorance)%20
    Processing Record 234 of set5 | Interstellar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Interstellar%20
    Processing Record 235 of set5 | Unbroken 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Unbroken%20
    Processing Record 236 of set5 | Whiplash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Whiplash%20
    Processing Record 237 of set5 | Captain America: The Winter Soldier 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Captain%20America:%20The%20Winter%20Soldier%20
    Processing Record 238 of set5 | Dawn of the Planet of the Apes 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Dawn%20of%20the%20Planet%20of%20the%20Apes%20
    Processing Record 239 of set5 | Guardians of the Galaxy 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Guardians%20of%20the%20Galaxy%20
    Processing Record 240 of set5 | Interstellar 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Interstellar%20
    Processing Record 1 of set6 | X-Men: Days of Future Past 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=X-Men:%20Days%20of%20Future%20Past%20
    Processing Record 2 of set6 | American Sniper 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=American%20Sniper%20
    Processing Record 3 of set6 | The Imitation Game 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Imitation%20Game%20
    Processing Record 4 of set6 | Inherent Vice 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inherent%20Vice%20
    Processing Record 5 of set6 | The Theory of Everything 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Theory%20of%20Everything%20
    Processing Record 6 of set6 | Whiplash 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Whiplash%20
    Processing Record 7 of set6 | Birdman or (The Unexpected Virtue of Ignorance) 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Birdman%20or%20(The%20Unexpected%20Virtue%20of%20Ignorance)%20
    Processing Record 8 of set6 | Boyhood 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Boyhood%20
    Processing Record 9 of set6 | Foxcatcher 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Foxcatcher%20
    Processing Record 10 of set6 | The Grand Budapest Hotel 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Grand%20Budapest%20Hotel%20
    Processing Record 11 of set6 | Nightcrawler 
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Nightcrawler%20
    Processing Record 12 of set6 | Harry Belafonte
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Harry%20Belafonte
    Processing Record 13 of set6 | Jean-Claude Carrière
    <class 'IndexError'>
    list index out of range
    Processing Record 14 of set6 | Hayao Miyazaki
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Hayao%20Miyazaki
    Processing Record 15 of set6 | Maureen O'Hara
    <class 'IndexError'>
    list index out of range
    Processing Record 16 of set6 | David Winchester Gray
    <class 'IndexError'>
    list index out of range
    Processing Record 17 of set6 | Steven Tiffen, Jeff Cohen and Michael Fecik
    <class 'IndexError'>
    list index out of range
    Processing Record 18 of set6 | Bryan Cranston
    <class 'IndexError'>
    list index out of range
    Processing Record 19 of set6 | Matt Damon
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Matt%20Damon
    Processing Record 20 of set6 | Leonardo DiCaprio
    <class 'IndexError'>
    list index out of range
    Processing Record 21 of set6 | Michael Fassbender
    <class 'IndexError'>
    list index out of range
    Processing Record 22 of set6 | Eddie Redmayne
    <class 'IndexError'>
    list index out of range
    Processing Record 23 of set6 | Christian Bale
    <class 'IndexError'>
    list index out of range
    Processing Record 24 of set6 | Tom Hardy
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Tom%20Hardy
    Processing Record 25 of set6 | Mark Ruffalo
    <class 'IndexError'>
    list index out of range
    Processing Record 26 of set6 | Mark Rylance
    <class 'IndexError'>
    list index out of range
    Processing Record 27 of set6 | Sylvester Stallone
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sylvester%20Stallone
    Processing Record 28 of set6 | Cate Blanchett
    <class 'IndexError'>
    list index out of range
    Processing Record 29 of set6 | Brie Larson
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brie%20Larson
    Processing Record 30 of set6 | Jennifer Lawrence
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Jennifer%20Lawrence
    Processing Record 31 of set6 | Charlotte Rampling
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Charlotte%20Rampling
    Processing Record 32 of set6 | Saoirse Ronan
    <class 'IndexError'>
    list index out of range
    Processing Record 33 of set6 | Jennifer Jason Leigh
    <class 'IndexError'>
    list index out of range
    Processing Record 34 of set6 | Rooney Mara
    <class 'IndexError'>
    list index out of range
    Processing Record 35 of set6 | Rachel McAdams
    <class 'IndexError'>
    list index out of range
    Processing Record 36 of set6 | Alicia Vikander
    <class 'IndexError'>
    list index out of range
    Processing Record 37 of set6 | Kate Winslet
    <class 'IndexError'>
    list index out of range
    Processing Record 38 of set6 | Anomalisa
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Anomalisa
    Processing Record 39 of set6 | Boy and the World
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Boy%20and%20the%20World
    Processing Record 40 of set6 | Inside Out
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inside%20Out
    Processing Record 41 of set6 | Shaun the Sheep Movie
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Shaun%20the%20Sheep%20Movie
    Processing Record 42 of set6 | When Marnie Was There
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=When%20Marnie%20Was%20There
    Processing Record 43 of set6 | Carol
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Carol
    Processing Record 44 of set6 | The Hateful Eight
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hateful%20Eight
    Processing Record 45 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 46 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 47 of set6 | Sicario
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sicario
    Processing Record 48 of set6 | Carol
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Carol
    Processing Record 49 of set6 | Cinderella
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Cinderella
    Processing Record 50 of set6 | The Danish Girl
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Danish%20Girl
    Processing Record 51 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 52 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 53 of set6 | The Big Short
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Big%20Short
    Processing Record 54 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 55 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 56 of set6 | Room
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Room
    Processing Record 57 of set6 | Spotlight
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Spotlight
    Processing Record 58 of set6 | Amy
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Amy
    Processing Record 59 of set6 | Cartel Land
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Cartel%20Land
    Processing Record 60 of set6 | The Look of Silence
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Look%20of%20Silence
    Processing Record 61 of set6 | What Happened, Miss Simone?
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=What%20Happened,%20Miss%20Simone?
    Processing Record 62 of set6 | Winter on Fire: Ukraine's Fight for Freedom
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Winter%20on%20Fire:%20Ukraine's%20Fight%20for%20Freedom
    Processing Record 63 of set6 | Body Team 12
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Body%20Team%2012
    Processing Record 64 of set6 | Chau, Beyond the Lines
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Chau,%20Beyond%20the%20Lines
    Processing Record 65 of set6 | Claude Lanzmann: Spectres of the Shoah
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Claude%20Lanzmann:%20Spectres%20of%20the%20Shoah
    Processing Record 66 of set6 | A Girl in the River: The Price of Forgiveness
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20Girl%20in%20the%20River:%20The%20Price%20of%20Forgiveness
    Processing Record 67 of set6 | Last Day of Freedom
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Last%20Day%20of%20Freedom
    Processing Record 68 of set6 | The Big Short
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Big%20Short
    Processing Record 69 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 70 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 71 of set6 | Spotlight
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Spotlight
    Processing Record 72 of set6 | Star Wars: The Force Awakens
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Wars:%20The%20Force%20Awakens
    Processing Record 73 of set6 | Embrace of the Serpent
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Embrace%20of%20the%20Serpent
    Processing Record 74 of set6 | Mustang
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mustang
    Processing Record 75 of set6 | Son of Saul
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Son%20of%20Saul
    Processing Record 76 of set6 | Theeb
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Theeb
    Processing Record 77 of set6 | A War
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=A%20War
    Processing Record 78 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 79 of set6 | The 100-Year-Old Man Who Climbed Out the Window and Disappeared
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20100-Year-Old%20Man%20Who%20Climbed%20Out%20the%20Window%20and%20Disappeared
    Processing Record 80 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 81 of set6 | Bridge of Spies
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bridge%20of%20Spies
    Processing Record 82 of set6 | Carol
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Carol
    Processing Record 83 of set6 | The Hateful Eight
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Hateful%20Eight
    Processing Record 84 of set6 | Sicario
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sicario
    Processing Record 85 of set6 | Star Wars: The Force Awakens
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Wars:%20The%20Force%20Awakens
    Processing Record 86 of set6 | "Earned It" from Fifty Shades of Grey
    <class 'IndexError'>
    list index out of range
    Processing Record 87 of set6 | Manta Ray from Racing Extinction
    <class 'IndexError'>
    list index out of range
    Processing Record 88 of set6 | Simple Song #3 from Youth
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Simple%20Song%20#3%20from%20Youth
    Processing Record 89 of set6 | "Til It Happens To You" from The Hunting Ground
    <class 'IndexError'>
    list index out of range
    Processing Record 90 of set6 | Writing's On The Wall from Spectre
    <class 'IndexError'>
    list index out of range
    Processing Record 91 of set6 | The Big Short
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Big%20Short
    Processing Record 92 of set6 | Bridge of Spies
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bridge%20of%20Spies
    Processing Record 93 of set6 | Brooklyn
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brooklyn
    Processing Record 94 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 95 of set6 | The Martian
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Martian
    Processing Record 96 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 97 of set6 | Room
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Room
    Processing Record 98 of set6 | Spotlight
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Spotlight
    Processing Record 99 of set6 | Bridge of Spies
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bridge%20of%20Spies
    Processing Record 100 of set6 | The Danish Girl
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Danish%20Girl
    Processing Record 101 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 102 of set6 | The Martian
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Martian
    Processing Record 103 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 104 of set6 | Bear Story
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bear%20Story
    Processing Record 105 of set6 | Prologue
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Prologue
    Processing Record 106 of set6 | Sanjay's Super Team
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sanjay's%20Super%20Team
    Processing Record 107 of set6 | We Can't Live without Cosmos
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=We%20Can't%20Live%20without%20Cosmos
    Processing Record 108 of set6 | World of Tomorrow
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=World%20of%20Tomorrow
    Processing Record 109 of set6 | Ave Maria
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ave%20Maria
    Processing Record 110 of set6 | Day One
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Day%20One
    Processing Record 111 of set6 | Everything Will Be Okay (Alles Wird Gut)
    <class 'IndexError'>
    list index out of range
    Processing Record 112 of set6 | Shok
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Shok
    Processing Record 113 of set6 | Stutterer
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Stutterer
    Processing Record 114 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 115 of set6 | The Martian
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Martian
    Processing Record 116 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 117 of set6 | Sicario
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Sicario
    Processing Record 118 of set6 | Star Wars: The Force Awakens
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Wars:%20The%20Force%20Awakens
    Processing Record 119 of set6 | Bridge of Spies
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bridge%20of%20Spies
    Processing Record 120 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 121 of set6 | The Martian
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Martian
    Processing Record 122 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 123 of set6 | Star Wars: The Force Awakens
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Wars:%20The%20Force%20Awakens
    Processing Record 124 of set6 | Ex Machina
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ex%20Machina
    Processing Record 125 of set6 | Mad Max: Fury Road
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Mad%20Max:%20Fury%20Road
    Processing Record 126 of set6 | The Martian
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Martian
    Processing Record 127 of set6 | The Revenant
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Revenant
    Processing Record 128 of set6 | Star Wars: The Force Awakens
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Star%20Wars:%20The%20Force%20Awakens
    Processing Record 129 of set6 | The Big Short
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Big%20Short
    Processing Record 130 of set6 | Brooklyn
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Brooklyn
    Processing Record 131 of set6 | Carol
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Carol
    Processing Record 132 of set6 | The Martian
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=The%20Martian
    Processing Record 133 of set6 | Room
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Room
    Processing Record 134 of set6 | Bridge of Spies
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Bridge%20of%20Spies
    Processing Record 135 of set6 | Ex Machina
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Ex%20Machina
    Processing Record 136 of set6 | Inside Out
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Inside%20Out
    Processing Record 137 of set6 | Spotlight
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Spotlight
    Processing Record 138 of set6 | Straight Outta Compton
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Straight%20Outta%20Compton
    Processing Record 139 of set6 | Debbie Reynolds
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Debbie%20Reynolds
    Processing Record 140 of set6 | Spike Lee
    https://api.themoviedb.org/3/search/movie?api_key=98e159931ae83a9fde8ba0f8c795951d&query=Spike%20Lee
    Processing Record 141 of set6 | Gena Rowlands
    <class 'IndexError'>
    list index out of range
    ------------------------------ 
     End of Data Retrieval 
    ------------------------------
    251
    


```python
print(id_list)
print(len(id_list))
```

    [525863, 450945, 43939, 403011, 30250, 265648, 493597, 4935, 3933, 533, 3291, 674, 254, 1904, 234200, 272, 142, 3291, 1904, 496274, 118, 1904, 10773, 234200, 69, 142, 398, 1640, 3291, 612, 415253, 13020, 1667, 14278, 29044, 214187, 245014, 245016, 245013, 921, 1985, 1640, 612, 69, 401157, 11661, 67, 2117, 868, 411, 921, 1895, 142, 1985, 1904, 612, 234200, 142, 398, 1640, 3291, 612, 220867, 44360, 52762, 12244, 13933, 12225, 104062, 47054, 25126, 254, 1904, 74, 411, 254, 1904, 69, 74, 411, 254, 74, 142, 398, 1985, 59, 612, 1640, 3291, 116, 10707, 231, 9526, 480748, 535954, 468473, 413131, 17159, 493597, 296273, 920, 9836, 9297, 1125, 1247, 1417, 58, 1124, 9676, 9693, 1491, 1417, 1124, 1494, 350, 1125, 1887, 1165, 1164, 1422, 1251, 1165, 9829, 184346, 1781, 34389, 1776, 514248, 170057, 58919, 245020, 13428, 1164, 1372, 9693, 1422, 9829, 3549, 2016, 582, 1417, 399055, 1579, 9339, 1417, 1164, 182, 1259, 1417, 1165, 1164, 1422, 1251, 773, 1165, 38635, 13060, 38580, 279550, 46247, 245017, 118796, 551296, 31073, 1579, 1372, 3683, 1251, 58, 1579, 1372, 1125, 3683, 58, 58, 503, 1452, 496, 9693, 1422, 1440, 1259, 1164, 1251, 773, 1417, 1165, 219711, 517261, 403011, 279843, 328481, 558398, 2011, 2062, 9408, 4982, 4347, 2268, 13885, 7345, 4512, 4347, 2013, 6977, 7345, 4688, 4347, 4517, 1407, 13885, 2013, 7326, 4566, 6977, 7345, 12901, 34981, 2359, 13362, 16666, 306745, 356270, 245026, 245031, 2503, 2013, 5915, 6977, 7345, 15048, 246777, 13614, 12246, 20714, 1407, 9757, 285, 4347, 7979, 4566, 2062, 5176, 4347, 7326, 4566, 6977, 7345, 159145, 35253, 10693, 1593, 162656, 245024, 2503, 6977, 2062, 7345, 1858, 2503, 6977, 2062, 5176, 1858, 2268, 285, 1858, 4347, 1919, 2013, 6977, 7345, 7326, 6615, 4566, 2062, 8272, 385851, 450945, 361776, 51828, 13053, 9502, 10673, 3580, 4922, 155, 12783, 4148, 3580, 4922, 155, 8055, 12405, 6972, 4922, 12783, 10139, 4148, 4922, 11499, 10139, 8055, 12405, 40215, 12172, 11236, 14048, 22319, 245032, 245034, 129235, 245035, 4922, 155, 11499, 10139, 12405, 6968, 63193, 375785, 15451, 8885, 4922, 155, 11253, 4922, 13813, 10139, 12405, 10673, 4922, 11499, 10139, 8055, 12405, 20722, 149117, 46343, 13042, 86118, 200618, 95608, 9447, 23764, 155, 1726, 12405, 10673, 8909, 4922, 155, 12405, 10673, 8909, 4922, 155, 1726, 4922, 14359, 11499, 8055, 12405, 10183, 10503, 8321, 10139, 10673, 18331, 403011, 522827, 393640, 371516, 306048, 9963, 296273, 162316, 14836, 10315, 10198, 26963, 14160, 19995, 8054, 10197, 10528, 18320, 19995, 767, 12162, 16869, 37903, 29963, 11156, 8054, 10197, 18320, 19995, 12162, 16869, 25793, 22947, 26763, 23128, 18570, 34576, 55204, 82248, 245037, 37098, 154576, 129427, 19995, 17654, 12162, 16869, 25793, 24424, 28644, 454610, 25376, 37903, 8832, 13475, 18320, 19995, 10315, 12162, 10528, 14160, 19995, 22881, 17654, 24684, 12162, 16869, 25793, 12573, 14160, 22947, 37845, 57091, 62967, 32389, 14447, 10591, 161679, 433618, 56047, 47798, 19995, 12162, 16869, 13475, 14160, 19995, 12162, 16869, 13475, 8373, 19995, 17654, 13475, 17654, 24684, 19833, 25793, 22947, 12162, 16869, 28089, 12573, 14160, 479518, 256132, 300302, 393640, 26058, 373721, 298545, 10191, 1491, 10193, 12155, 12444, 27205, 45269, 44264, 44214, 27205, 45269, 37799, 44264, 12155, 370964, 45269, 44638, 44264, 44214, 45317, 45269, 37799, 44264, 39452, 40663, 44639, 39312, 46689, 128602, 82421, 113366, 193504, 245038, 44214, 45317, 45269, 44115, 37799, 45958, 38810, 44716, 46738, 47904, 46829, 147773, 7978, 10191, 27205, 45269, 44115, 37799, 44214, 45317, 27205, 39781, 45269, 44115, 37799, 10193, 44264, 39013, 137, 28118, 159523, 58515, 30998, 33408, 195487, 95468, 159508, 27205, 10193, 20526, 44264, 44048, 27205, 45269, 27576, 37799, 44264, 12155, 12444, 44603, 27205, 10138, 44115, 37799, 10193, 44264, 39013, 44009, 45317, 27205, 39781, 45269, 187156, 4539, 403011, 373895, 104156, 306048, 277660, 52264, 63498, 49444, 417859, 44896, 74643, 12445, 44826, 59436, 57212, 74643, 65754, 44826, 8967, 57212, 61891, 74643, 44826, 38684, 80591, 74643, 65057, 44826, 59436, 8967, 74310, 79042, 83660, 57276, 82620, 89194, 103528, 89196, 19316, 84346, 74643, 65057, 65754, 44826, 60308, 63310, 72551, 417643, 78480, 60243, 73873, 12445, 71688, 17578, 74643, 44826, 49517, 57212, 74643, 65057, 64685, 50014, 44826, 59436, 60308, 8967, 57212, 9563, 86412, 30636, 91516, 368940, 99581, 528765, 465381, 451925, 92190, 64690, 65754, 44826, 38356, 57212, 65754, 44826, 60308, 38356, 57212, 12445, 44826, 39254, 61791, 38356, 65057, 44826, 10316, 60308, 49517, 74643, 55721, 50839, 59436, 60243, 26132, 256521, 566838, 43939, 304533, 248829, 373721, 51828, 62177, 62214, 77174, 72197, 82690, 96724, 68718, 87827, 72976, 37724, 96724, 82695, 72976, 62764, 58595, 86837, 84175, 87827, 72976, 82693, 84170, 127918, 84286, 84288, 84334, 30671, 137651, 137652, 80291, 278, 68734, 87827, 72976, 82693, 97630, 86837, 70667, 646, 88273, 98205, 112336, 49051, 82695, 96724, 68734, 87827, 72976, 37724, 86837, 68734, 84175, 68718, 82695, 87827, 72976, 82693, 97630, 96724, 49051, 82695, 87827, 72976, 157301, 142563, 24940, 116440, 140420, 146891, 146892, 157289, 325348, 68734, 68718, 87827, 37724, 97630, 68734, 82695, 87827, 72976, 37724, 49051, 87827, 24428, 70981, 58595, 68734, 84175, 87827, 72976, 82693, 86837, 68718, 87502, 83666, 97630, 541295, 515632, 299947, 533864, 9963, 493597, 373721, 552691, 49519, 93456, 126319, 109445, 149870, 44865, 49047, 86829, 129670, 146233, 168672, 44865, 64682, 111473, 76203, 168672, 49047, 129670, 76203, 106646, 123678, 159002, 159004, 401246, 159014, 249714, 249719, 249721, 443313, 249726, 168672, 109424, 152532, 49047, 76203, 137182, 247794, 371645, 186997, 68178, 152532, 208134, 57201, 203833, 49047, 152601, 205220, 140823, 168672, 109424, 152532, 49047, 152601, 129670, 205220, 76203, 106646, 168672, 49047, 64682, 152601, 76203, 436494, 234567, 234862, 323665, 152581, 222796, 249699, 200942, 152747, 109424, 49047, 57158, 193756, 109424, 49047, 57158, 86829, 193756, 49047, 57158, 68721, 57201, 54138, 132344, 109424, 205220, 76203, 106646, 168672, 160588, 152532, 152601, 129670, 456881, 162637, 459800, 339410, 177572, 170687, 82702, 110416, 149871, 194662, 120467, 209274, 245700, 227306, 120467, 171274, 224141, 102651, 245700, 194662, 85350, 87492, 120467, 205596, 293310, 169607, 250761, 23620, 263614, 248808, 300176, 274805, 259520, 190859, 85350, 120467, 205596, 244786, 209274, 14372, 238628, 265228, 265195, 87492, 120467, 118340, 120467, 205596, 157336, 245700, 266856, 190859, 194662, 85350, 120467, 205596, 273895, 266856, 244786, 120467, 205596, 157336, 224141, 245700, 307695, 254273, 293299, 289024, 289280, 550826, 307686, 307692, 220809, 190859, 194662, 122917, 157336, 227306, 190859, 194662, 157336, 227306, 244786, 100402, 119450, 118340, 157336, 127585, 190859, 205596, 171274, 266856, 244786, 194662, 85350, 87492, 120467, 242582, 91367, 452630, 371516, 42299, 10477, 531352, 373721, 82673, 291270, 223706, 150540, 263109, 242828, 258480, 273248, 76341, 281957, 273481, 258480, 150689, 306819, 76341, 281957, 318846, 76341, 281957, 264644, 314365, 331781, 317952, 267480, 318044, 355020, 365447, 369362, 369363, 369364, 369366, 318846, 76341, 281957, 314365, 140607, 336808, 336804, 336050, 287628, 475132, 76341, 145247, 281957, 296098, 258480, 273248, 273481, 140607, 547766, 318846, 296098, 167073, 76341, 286217, 281957, 264644, 314365, 296098, 306819, 76341, 286217, 281957, 351981, 359549, 345637, 329063, 303867, 348396, 51828, 366736, 369373, 76341, 286217, 281957, 273481, 140607, 296098, 76341, 286217, 281957, 140607, 264660, 76341, 286217, 281957, 140607, 318846, 167073, 258480, 286217, 264644, 296098, 264660, 150540, 314365, 277216, 398738, 9469]
    1090
    


```python
url2 = "https://api.themoviedb.org/3/movie/"

api_key = "api_key=98e159931ae83a9fde8ba0f8c795951d"
payload = "{}"
```


```python
movies_df = pd.DataFrame(columns = ["Movie", "Release Date","Budget", "Revenue", "Genres"])
call_count = 1
sets = 1
error_count2 = 0
index = 0
movies_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Movie</th>
      <th>Release Date</th>
      <th>Budget</th>
      <th>Revenue</th>
      <th>Genres</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
for x in id_list:
    try:
        print(f'Processing Record {call_count} of set{sets} | {x}')
        print(url2)
        response = requests.request("GET", url2 + str(x) + "?&" + api_key, data=payload)
        json_data = response.json()
        movies_df.set_value(index, "Movie", json_data['original_title'])
        movies_df.set_value(index, "Release Date", json_data['release_date'])
        movies_df.set_value(index, "Revenue", json_data['revenue'])
        movies_df.set_value(index, "Budget", json_data['budget'])
        movies_df.set_value(index,"Genres", (json_data['genres'][0])['name'])
        index = index + 1
    except Exception as e:
        print(type(e))
        print(str(e))
        error_count2 = error_count2 + 1
    call_count = call_count + 1
    if call_count == 240:
        call_count1 = 1
        sets = sets + 1
        time.sleep(60)
print(f'------------------------------ \n End of Data Retrieval \n------------------------------')
print(error_count)
```

    Processing Record 1 of set1 | 525863
    https://api.themoviedb.org/3/movie/
    

    c:\users\jorge\anaconda3\envs\myenvironment\lib\site-packages\ipykernel_launcher.py:7: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
      import sys
    c:\users\jorge\anaconda3\envs\myenvironment\lib\site-packages\ipykernel_launcher.py:8: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
      
    c:\users\jorge\anaconda3\envs\myenvironment\lib\site-packages\ipykernel_launcher.py:9: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
      if __name__ == '__main__':
    c:\users\jorge\anaconda3\envs\myenvironment\lib\site-packages\ipykernel_launcher.py:10: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
      # Remove the CWD from sys.path while we load stuff.
    c:\users\jorge\anaconda3\envs\myenvironment\lib\site-packages\ipykernel_launcher.py:11: FutureWarning: set_value is deprecated and will be removed in a future release. Please use .at[] or .iat[] accessors instead
      # This is added back by InteractiveShellApp.init_path()
    

    Processing Record 2 of set1 | 450945
    https://api.themoviedb.org/3/movie/
    Processing Record 3 of set1 | 43939
    https://api.themoviedb.org/3/movie/
    Processing Record 4 of set1 | 403011
    https://api.themoviedb.org/3/movie/
    Processing Record 5 of set1 | 30250
    https://api.themoviedb.org/3/movie/
    Processing Record 6 of set1 | 265648
    https://api.themoviedb.org/3/movie/
    Processing Record 7 of set1 | 493597
    https://api.themoviedb.org/3/movie/
    Processing Record 8 of set1 | 4935
    https://api.themoviedb.org/3/movie/
    Processing Record 9 of set1 | 3933
    https://api.themoviedb.org/3/movie/
    Processing Record 10 of set1 | 533
    https://api.themoviedb.org/3/movie/
    Processing Record 11 of set1 | 3291
    https://api.themoviedb.org/3/movie/
    Processing Record 12 of set1 | 674
    https://api.themoviedb.org/3/movie/
    Processing Record 13 of set1 | 254
    https://api.themoviedb.org/3/movie/
    Processing Record 14 of set1 | 1904
    https://api.themoviedb.org/3/movie/
    Processing Record 15 of set1 | 234200
    https://api.themoviedb.org/3/movie/
    Processing Record 16 of set1 | 272
    https://api.themoviedb.org/3/movie/
    Processing Record 17 of set1 | 142
    https://api.themoviedb.org/3/movie/
    Processing Record 18 of set1 | 3291
    https://api.themoviedb.org/3/movie/
    Processing Record 19 of set1 | 1904
    https://api.themoviedb.org/3/movie/
    Processing Record 20 of set1 | 496274
    https://api.themoviedb.org/3/movie/
    Processing Record 21 of set1 | 118
    https://api.themoviedb.org/3/movie/
    Processing Record 22 of set1 | 1904
    https://api.themoviedb.org/3/movie/
    Processing Record 23 of set1 | 10773
    https://api.themoviedb.org/3/movie/
    Processing Record 24 of set1 | 234200
    https://api.themoviedb.org/3/movie/
    Processing Record 25 of set1 | 69
    https://api.themoviedb.org/3/movie/
    Processing Record 26 of set1 | 142
    https://api.themoviedb.org/3/movie/
    Processing Record 27 of set1 | 398
    https://api.themoviedb.org/3/movie/
    Processing Record 28 of set1 | 1640
    https://api.themoviedb.org/3/movie/
    Processing Record 29 of set1 | 3291
    https://api.themoviedb.org/3/movie/
    Processing Record 30 of set1 | 612
    https://api.themoviedb.org/3/movie/
    Processing Record 31 of set1 | 415253
    https://api.themoviedb.org/3/movie/
    Processing Record 32 of set1 | 13020
    https://api.themoviedb.org/3/movie/
    Processing Record 33 of set1 | 1667
    https://api.themoviedb.org/3/movie/
    Processing Record 34 of set1 | 14278
    https://api.themoviedb.org/3/movie/
    Processing Record 35 of set1 | 29044
    https://api.themoviedb.org/3/movie/
    Processing Record 36 of set1 | 214187
    https://api.themoviedb.org/3/movie/
    Processing Record 37 of set1 | 245014
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 38 of set1 | 245016
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 39 of set1 | 245013
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 40 of set1 | 921
    https://api.themoviedb.org/3/movie/
    Processing Record 41 of set1 | 1985
    https://api.themoviedb.org/3/movie/
    Processing Record 42 of set1 | 1640
    https://api.themoviedb.org/3/movie/
    Processing Record 43 of set1 | 612
    https://api.themoviedb.org/3/movie/
    Processing Record 44 of set1 | 69
    https://api.themoviedb.org/3/movie/
    Processing Record 45 of set1 | 401157
    https://api.themoviedb.org/3/movie/
    Processing Record 46 of set1 | 11661
    https://api.themoviedb.org/3/movie/
    Processing Record 47 of set1 | 67
    https://api.themoviedb.org/3/movie/
    Processing Record 48 of set1 | 2117
    https://api.themoviedb.org/3/movie/
    Processing Record 49 of set1 | 868
    https://api.themoviedb.org/3/movie/
    Processing Record 50 of set1 | 411
    https://api.themoviedb.org/3/movie/
    Processing Record 51 of set1 | 921
    https://api.themoviedb.org/3/movie/
    Processing Record 52 of set1 | 1895
    https://api.themoviedb.org/3/movie/
    Processing Record 53 of set1 | 142
    https://api.themoviedb.org/3/movie/
    Processing Record 54 of set1 | 1985
    https://api.themoviedb.org/3/movie/
    Processing Record 55 of set1 | 1904
    https://api.themoviedb.org/3/movie/
    Processing Record 56 of set1 | 612
    https://api.themoviedb.org/3/movie/
    Processing Record 57 of set1 | 234200
    https://api.themoviedb.org/3/movie/
    Processing Record 58 of set1 | 142
    https://api.themoviedb.org/3/movie/
    Processing Record 59 of set1 | 398
    https://api.themoviedb.org/3/movie/
    Processing Record 60 of set1 | 1640
    https://api.themoviedb.org/3/movie/
    Processing Record 61 of set1 | 3291
    https://api.themoviedb.org/3/movie/
    Processing Record 62 of set1 | 612
    https://api.themoviedb.org/3/movie/
    Processing Record 63 of set1 | 220867
    https://api.themoviedb.org/3/movie/
    Processing Record 64 of set1 | 44360
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 65 of set1 | 52762
    https://api.themoviedb.org/3/movie/
    Processing Record 66 of set1 | 12244
    https://api.themoviedb.org/3/movie/
    Processing Record 67 of set1 | 13933
    https://api.themoviedb.org/3/movie/
    Processing Record 68 of set1 | 12225
    https://api.themoviedb.org/3/movie/
    Processing Record 69 of set1 | 104062
    https://api.themoviedb.org/3/movie/
    Processing Record 70 of set1 | 47054
    https://api.themoviedb.org/3/movie/
    Processing Record 71 of set1 | 25126
    https://api.themoviedb.org/3/movie/
    Processing Record 72 of set1 | 254
    https://api.themoviedb.org/3/movie/
    Processing Record 73 of set1 | 1904
    https://api.themoviedb.org/3/movie/
    Processing Record 74 of set1 | 74
    https://api.themoviedb.org/3/movie/
    Processing Record 75 of set1 | 411
    https://api.themoviedb.org/3/movie/
    Processing Record 76 of set1 | 254
    https://api.themoviedb.org/3/movie/
    Processing Record 77 of set1 | 1904
    https://api.themoviedb.org/3/movie/
    Processing Record 78 of set1 | 69
    https://api.themoviedb.org/3/movie/
    Processing Record 79 of set1 | 74
    https://api.themoviedb.org/3/movie/
    Processing Record 80 of set1 | 411
    https://api.themoviedb.org/3/movie/
    Processing Record 81 of set1 | 254
    https://api.themoviedb.org/3/movie/
    Processing Record 82 of set1 | 74
    https://api.themoviedb.org/3/movie/
    Processing Record 83 of set1 | 142
    https://api.themoviedb.org/3/movie/
    Processing Record 84 of set1 | 398
    https://api.themoviedb.org/3/movie/
    Processing Record 85 of set1 | 1985
    https://api.themoviedb.org/3/movie/
    Processing Record 86 of set1 | 59
    https://api.themoviedb.org/3/movie/
    Processing Record 87 of set1 | 612
    https://api.themoviedb.org/3/movie/
    Processing Record 88 of set1 | 1640
    https://api.themoviedb.org/3/movie/
    Processing Record 89 of set1 | 3291
    https://api.themoviedb.org/3/movie/
    Processing Record 90 of set1 | 116
    https://api.themoviedb.org/3/movie/
    Processing Record 91 of set1 | 10707
    https://api.themoviedb.org/3/movie/
    Processing Record 92 of set1 | 231
    https://api.themoviedb.org/3/movie/
    Processing Record 93 of set1 | 9526
    https://api.themoviedb.org/3/movie/
    Processing Record 94 of set1 | 480748
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 95 of set1 | 535954
    https://api.themoviedb.org/3/movie/
    Processing Record 96 of set1 | 468473
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 97 of set1 | 413131
    https://api.themoviedb.org/3/movie/
    Processing Record 98 of set1 | 17159
    https://api.themoviedb.org/3/movie/
    Processing Record 99 of set1 | 493597
    https://api.themoviedb.org/3/movie/
    Processing Record 100 of set1 | 296273
    https://api.themoviedb.org/3/movie/
    Processing Record 101 of set1 | 920
    https://api.themoviedb.org/3/movie/
    Processing Record 102 of set1 | 9836
    https://api.themoviedb.org/3/movie/
    Processing Record 103 of set1 | 9297
    https://api.themoviedb.org/3/movie/
    Processing Record 104 of set1 | 1125
    https://api.themoviedb.org/3/movie/
    Processing Record 105 of set1 | 1247
    https://api.themoviedb.org/3/movie/
    Processing Record 106 of set1 | 1417
    https://api.themoviedb.org/3/movie/
    Processing Record 107 of set1 | 58
    https://api.themoviedb.org/3/movie/
    Processing Record 108 of set1 | 1124
    https://api.themoviedb.org/3/movie/
    Processing Record 109 of set1 | 9676
    https://api.themoviedb.org/3/movie/
    Processing Record 110 of set1 | 9693
    https://api.themoviedb.org/3/movie/
    Processing Record 111 of set1 | 1491
    https://api.themoviedb.org/3/movie/
    Processing Record 112 of set1 | 1417
    https://api.themoviedb.org/3/movie/
    Processing Record 113 of set1 | 1124
    https://api.themoviedb.org/3/movie/
    Processing Record 114 of set1 | 1494
    https://api.themoviedb.org/3/movie/
    Processing Record 115 of set1 | 350
    https://api.themoviedb.org/3/movie/
    Processing Record 116 of set1 | 1125
    https://api.themoviedb.org/3/movie/
    Processing Record 117 of set1 | 1887
    https://api.themoviedb.org/3/movie/
    Processing Record 118 of set1 | 1165
    https://api.themoviedb.org/3/movie/
    Processing Record 119 of set1 | 1164
    https://api.themoviedb.org/3/movie/
    Processing Record 120 of set1 | 1422
    https://api.themoviedb.org/3/movie/
    Processing Record 121 of set1 | 1251
    https://api.themoviedb.org/3/movie/
    Processing Record 122 of set1 | 1165
    https://api.themoviedb.org/3/movie/
    Processing Record 123 of set1 | 9829
    https://api.themoviedb.org/3/movie/
    Processing Record 124 of set1 | 184346
    https://api.themoviedb.org/3/movie/
    Processing Record 125 of set1 | 1781
    https://api.themoviedb.org/3/movie/
    Processing Record 126 of set1 | 34389
    https://api.themoviedb.org/3/movie/
    Processing Record 127 of set1 | 1776
    https://api.themoviedb.org/3/movie/
    Processing Record 128 of set1 | 514248
    https://api.themoviedb.org/3/movie/
    Processing Record 129 of set1 | 170057
    https://api.themoviedb.org/3/movie/
    Processing Record 130 of set1 | 58919
    https://api.themoviedb.org/3/movie/
    Processing Record 131 of set1 | 245020
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 132 of set1 | 13428
    https://api.themoviedb.org/3/movie/
    Processing Record 133 of set1 | 1164
    https://api.themoviedb.org/3/movie/
    Processing Record 134 of set1 | 1372
    https://api.themoviedb.org/3/movie/
    Processing Record 135 of set1 | 9693
    https://api.themoviedb.org/3/movie/
    Processing Record 136 of set1 | 1422
    https://api.themoviedb.org/3/movie/
    Processing Record 137 of set1 | 9829
    https://api.themoviedb.org/3/movie/
    Processing Record 138 of set1 | 3549
    https://api.themoviedb.org/3/movie/
    Processing Record 139 of set1 | 2016
    https://api.themoviedb.org/3/movie/
    Processing Record 140 of set1 | 582
    https://api.themoviedb.org/3/movie/
    Processing Record 141 of set1 | 1417
    https://api.themoviedb.org/3/movie/
    Processing Record 142 of set1 | 399055
    https://api.themoviedb.org/3/movie/
    Processing Record 143 of set1 | 1579
    https://api.themoviedb.org/3/movie/
    Processing Record 144 of set1 | 9339
    https://api.themoviedb.org/3/movie/
    Processing Record 145 of set1 | 1417
    https://api.themoviedb.org/3/movie/
    Processing Record 146 of set1 | 1164
    https://api.themoviedb.org/3/movie/
    Processing Record 147 of set1 | 182
    https://api.themoviedb.org/3/movie/
    Processing Record 148 of set1 | 1259
    https://api.themoviedb.org/3/movie/
    Processing Record 149 of set1 | 1417
    https://api.themoviedb.org/3/movie/
    Processing Record 150 of set1 | 1165
    https://api.themoviedb.org/3/movie/
    Processing Record 151 of set1 | 1164
    https://api.themoviedb.org/3/movie/
    Processing Record 152 of set1 | 1422
    https://api.themoviedb.org/3/movie/
    Processing Record 153 of set1 | 1251
    https://api.themoviedb.org/3/movie/
    Processing Record 154 of set1 | 773
    https://api.themoviedb.org/3/movie/
    Processing Record 155 of set1 | 1165
    https://api.themoviedb.org/3/movie/
    Processing Record 156 of set1 | 38635
    https://api.themoviedb.org/3/movie/
    Processing Record 157 of set1 | 13060
    https://api.themoviedb.org/3/movie/
    Processing Record 158 of set1 | 38580
    https://api.themoviedb.org/3/movie/
    Processing Record 159 of set1 | 279550
    https://api.themoviedb.org/3/movie/
    Processing Record 160 of set1 | 46247
    https://api.themoviedb.org/3/movie/
    Processing Record 161 of set1 | 245017
    https://api.themoviedb.org/3/movie/
    Processing Record 162 of set1 | 118796
    https://api.themoviedb.org/3/movie/
    Processing Record 163 of set1 | 551296
    https://api.themoviedb.org/3/movie/
    Processing Record 164 of set1 | 31073
    https://api.themoviedb.org/3/movie/
    Processing Record 165 of set1 | 1579
    https://api.themoviedb.org/3/movie/
    Processing Record 166 of set1 | 1372
    https://api.themoviedb.org/3/movie/
    Processing Record 167 of set1 | 3683
    https://api.themoviedb.org/3/movie/
    Processing Record 168 of set1 | 1251
    https://api.themoviedb.org/3/movie/
    Processing Record 169 of set1 | 58
    https://api.themoviedb.org/3/movie/
    Processing Record 170 of set1 | 1579
    https://api.themoviedb.org/3/movie/
    Processing Record 171 of set1 | 1372
    https://api.themoviedb.org/3/movie/
    Processing Record 172 of set1 | 1125
    https://api.themoviedb.org/3/movie/
    Processing Record 173 of set1 | 3683
    https://api.themoviedb.org/3/movie/
    Processing Record 174 of set1 | 58
    https://api.themoviedb.org/3/movie/
    Processing Record 175 of set1 | 58
    https://api.themoviedb.org/3/movie/
    Processing Record 176 of set1 | 503
    https://api.themoviedb.org/3/movie/
    Processing Record 177 of set1 | 1452
    https://api.themoviedb.org/3/movie/
    Processing Record 178 of set1 | 496
    https://api.themoviedb.org/3/movie/
    Processing Record 179 of set1 | 9693
    https://api.themoviedb.org/3/movie/
    Processing Record 180 of set1 | 1422
    https://api.themoviedb.org/3/movie/
    Processing Record 181 of set1 | 1440
    https://api.themoviedb.org/3/movie/
    Processing Record 182 of set1 | 1259
    https://api.themoviedb.org/3/movie/
    Processing Record 183 of set1 | 1164
    https://api.themoviedb.org/3/movie/
    Processing Record 184 of set1 | 1251
    https://api.themoviedb.org/3/movie/
    Processing Record 185 of set1 | 773
    https://api.themoviedb.org/3/movie/
    Processing Record 186 of set1 | 1417
    https://api.themoviedb.org/3/movie/
    Processing Record 187 of set1 | 1165
    https://api.themoviedb.org/3/movie/
    Processing Record 188 of set1 | 219711
    https://api.themoviedb.org/3/movie/
    Processing Record 189 of set1 | 517261
    https://api.themoviedb.org/3/movie/
    Processing Record 190 of set1 | 403011
    https://api.themoviedb.org/3/movie/
    Processing Record 191 of set1 | 279843
    https://api.themoviedb.org/3/movie/
    Processing Record 192 of set1 | 328481
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 193 of set1 | 558398
    https://api.themoviedb.org/3/movie/
    Processing Record 194 of set1 | 2011
    https://api.themoviedb.org/3/movie/
    Processing Record 195 of set1 | 2062
    https://api.themoviedb.org/3/movie/
    Processing Record 196 of set1 | 9408
    https://api.themoviedb.org/3/movie/
    Processing Record 197 of set1 | 4982
    https://api.themoviedb.org/3/movie/
    Processing Record 198 of set1 | 4347
    https://api.themoviedb.org/3/movie/
    Processing Record 199 of set1 | 2268
    https://api.themoviedb.org/3/movie/
    Processing Record 200 of set1 | 13885
    https://api.themoviedb.org/3/movie/
    Processing Record 201 of set1 | 7345
    https://api.themoviedb.org/3/movie/
    Processing Record 202 of set1 | 4512
    https://api.themoviedb.org/3/movie/
    Processing Record 203 of set1 | 4347
    https://api.themoviedb.org/3/movie/
    Processing Record 204 of set1 | 2013
    https://api.themoviedb.org/3/movie/
    Processing Record 205 of set1 | 6977
    https://api.themoviedb.org/3/movie/
    Processing Record 206 of set1 | 7345
    https://api.themoviedb.org/3/movie/
    Processing Record 207 of set1 | 4688
    https://api.themoviedb.org/3/movie/
    Processing Record 208 of set1 | 4347
    https://api.themoviedb.org/3/movie/
    Processing Record 209 of set1 | 4517
    https://api.themoviedb.org/3/movie/
    Processing Record 210 of set1 | 1407
    https://api.themoviedb.org/3/movie/
    Processing Record 211 of set1 | 13885
    https://api.themoviedb.org/3/movie/
    Processing Record 212 of set1 | 2013
    https://api.themoviedb.org/3/movie/
    Processing Record 213 of set1 | 7326
    https://api.themoviedb.org/3/movie/
    Processing Record 214 of set1 | 4566
    https://api.themoviedb.org/3/movie/
    Processing Record 215 of set1 | 6977
    https://api.themoviedb.org/3/movie/
    Processing Record 216 of set1 | 7345
    https://api.themoviedb.org/3/movie/
    Processing Record 217 of set1 | 12901
    https://api.themoviedb.org/3/movie/
    Processing Record 218 of set1 | 34981
    https://api.themoviedb.org/3/movie/
    Processing Record 219 of set1 | 2359
    https://api.themoviedb.org/3/movie/
    Processing Record 220 of set1 | 13362
    https://api.themoviedb.org/3/movie/
    Processing Record 221 of set1 | 16666
    https://api.themoviedb.org/3/movie/
    Processing Record 222 of set1 | 306745
    https://api.themoviedb.org/3/movie/
    Processing Record 223 of set1 | 356270
    https://api.themoviedb.org/3/movie/
    Processing Record 224 of set1 | 245026
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 225 of set1 | 245031
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 226 of set1 | 2503
    https://api.themoviedb.org/3/movie/
    Processing Record 227 of set1 | 2013
    https://api.themoviedb.org/3/movie/
    Processing Record 228 of set1 | 5915
    https://api.themoviedb.org/3/movie/
    Processing Record 229 of set1 | 6977
    https://api.themoviedb.org/3/movie/
    Processing Record 230 of set1 | 7345
    https://api.themoviedb.org/3/movie/
    Processing Record 231 of set1 | 15048
    https://api.themoviedb.org/3/movie/
    Processing Record 232 of set1 | 246777
    https://api.themoviedb.org/3/movie/
    Processing Record 233 of set1 | 13614
    https://api.themoviedb.org/3/movie/
    Processing Record 234 of set1 | 12246
    https://api.themoviedb.org/3/movie/
    Processing Record 235 of set1 | 20714
    https://api.themoviedb.org/3/movie/
    Processing Record 236 of set1 | 1407
    https://api.themoviedb.org/3/movie/
    Processing Record 237 of set1 | 9757
    https://api.themoviedb.org/3/movie/
    Processing Record 238 of set1 | 285
    https://api.themoviedb.org/3/movie/
    Processing Record 239 of set1 | 4347
    https://api.themoviedb.org/3/movie/
    Processing Record 240 of set2 | 7979
    https://api.themoviedb.org/3/movie/
    Processing Record 241 of set2 | 4566
    https://api.themoviedb.org/3/movie/
    Processing Record 242 of set2 | 2062
    https://api.themoviedb.org/3/movie/
    Processing Record 243 of set2 | 5176
    https://api.themoviedb.org/3/movie/
    Processing Record 244 of set2 | 4347
    https://api.themoviedb.org/3/movie/
    Processing Record 245 of set2 | 7326
    https://api.themoviedb.org/3/movie/
    Processing Record 246 of set2 | 4566
    https://api.themoviedb.org/3/movie/
    Processing Record 247 of set2 | 6977
    https://api.themoviedb.org/3/movie/
    Processing Record 248 of set2 | 7345
    https://api.themoviedb.org/3/movie/
    Processing Record 249 of set2 | 159145
    https://api.themoviedb.org/3/movie/
    Processing Record 250 of set2 | 35253
    https://api.themoviedb.org/3/movie/
    Processing Record 251 of set2 | 10693
    https://api.themoviedb.org/3/movie/
    Processing Record 252 of set2 | 1593
    https://api.themoviedb.org/3/movie/
    Processing Record 253 of set2 | 162656
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 254 of set2 | 245024
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 255 of set2 | 2503
    https://api.themoviedb.org/3/movie/
    Processing Record 256 of set2 | 6977
    https://api.themoviedb.org/3/movie/
    Processing Record 257 of set2 | 2062
    https://api.themoviedb.org/3/movie/
    Processing Record 258 of set2 | 7345
    https://api.themoviedb.org/3/movie/
    Processing Record 259 of set2 | 1858
    https://api.themoviedb.org/3/movie/
    Processing Record 260 of set2 | 2503
    https://api.themoviedb.org/3/movie/
    Processing Record 261 of set2 | 6977
    https://api.themoviedb.org/3/movie/
    Processing Record 262 of set2 | 2062
    https://api.themoviedb.org/3/movie/
    Processing Record 263 of set2 | 5176
    https://api.themoviedb.org/3/movie/
    Processing Record 264 of set2 | 1858
    https://api.themoviedb.org/3/movie/
    Processing Record 265 of set2 | 2268
    https://api.themoviedb.org/3/movie/
    Processing Record 266 of set2 | 285
    https://api.themoviedb.org/3/movie/
    Processing Record 267 of set2 | 1858
    https://api.themoviedb.org/3/movie/
    Processing Record 268 of set2 | 4347
    https://api.themoviedb.org/3/movie/
    Processing Record 269 of set2 | 1919
    https://api.themoviedb.org/3/movie/
    Processing Record 270 of set2 | 2013
    https://api.themoviedb.org/3/movie/
    Processing Record 271 of set2 | 6977
    https://api.themoviedb.org/3/movie/
    Processing Record 272 of set2 | 7345
    https://api.themoviedb.org/3/movie/
    Processing Record 273 of set2 | 7326
    https://api.themoviedb.org/3/movie/
    Processing Record 274 of set2 | 6615
    https://api.themoviedb.org/3/movie/
    Processing Record 275 of set2 | 4566
    https://api.themoviedb.org/3/movie/
    Processing Record 276 of set2 | 2062
    https://api.themoviedb.org/3/movie/
    Processing Record 277 of set2 | 8272
    https://api.themoviedb.org/3/movie/
    Processing Record 278 of set2 | 385851
    https://api.themoviedb.org/3/movie/
    Processing Record 279 of set2 | 450945
    https://api.themoviedb.org/3/movie/
    Processing Record 280 of set2 | 361776
    https://api.themoviedb.org/3/movie/
    Processing Record 281 of set2 | 51828
    https://api.themoviedb.org/3/movie/
    Processing Record 282 of set2 | 13053
    https://api.themoviedb.org/3/movie/
    Processing Record 283 of set2 | 9502
    https://api.themoviedb.org/3/movie/
    Processing Record 284 of set2 | 10673
    https://api.themoviedb.org/3/movie/
    Processing Record 285 of set2 | 3580
    https://api.themoviedb.org/3/movie/
    Processing Record 286 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 287 of set2 | 155
    https://api.themoviedb.org/3/movie/
    Processing Record 288 of set2 | 12783
    https://api.themoviedb.org/3/movie/
    Processing Record 289 of set2 | 4148
    https://api.themoviedb.org/3/movie/
    Processing Record 290 of set2 | 3580
    https://api.themoviedb.org/3/movie/
    Processing Record 291 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 292 of set2 | 155
    https://api.themoviedb.org/3/movie/
    Processing Record 293 of set2 | 8055
    https://api.themoviedb.org/3/movie/
    Processing Record 294 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 295 of set2 | 6972
    https://api.themoviedb.org/3/movie/
    Processing Record 296 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 297 of set2 | 12783
    https://api.themoviedb.org/3/movie/
    Processing Record 298 of set2 | 10139
    https://api.themoviedb.org/3/movie/
    Processing Record 299 of set2 | 4148
    https://api.themoviedb.org/3/movie/
    Processing Record 300 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 301 of set2 | 11499
    https://api.themoviedb.org/3/movie/
    Processing Record 302 of set2 | 10139
    https://api.themoviedb.org/3/movie/
    Processing Record 303 of set2 | 8055
    https://api.themoviedb.org/3/movie/
    Processing Record 304 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 305 of set2 | 40215
    https://api.themoviedb.org/3/movie/
    Processing Record 306 of set2 | 12172
    https://api.themoviedb.org/3/movie/
    Processing Record 307 of set2 | 11236
    https://api.themoviedb.org/3/movie/
    Processing Record 308 of set2 | 14048
    https://api.themoviedb.org/3/movie/
    Processing Record 309 of set2 | 22319
    https://api.themoviedb.org/3/movie/
    Processing Record 310 of set2 | 245032
    https://api.themoviedb.org/3/movie/
    Processing Record 311 of set2 | 245034
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 312 of set2 | 129235
    https://api.themoviedb.org/3/movie/
    Processing Record 313 of set2 | 245035
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 314 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 315 of set2 | 155
    https://api.themoviedb.org/3/movie/
    Processing Record 316 of set2 | 11499
    https://api.themoviedb.org/3/movie/
    Processing Record 317 of set2 | 10139
    https://api.themoviedb.org/3/movie/
    Processing Record 318 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 319 of set2 | 6968
    https://api.themoviedb.org/3/movie/
    Processing Record 320 of set2 | 63193
    https://api.themoviedb.org/3/movie/
    Processing Record 321 of set2 | 375785
    https://api.themoviedb.org/3/movie/
    Processing Record 322 of set2 | 15451
    https://api.themoviedb.org/3/movie/
    Processing Record 323 of set2 | 8885
    https://api.themoviedb.org/3/movie/
    Processing Record 324 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 325 of set2 | 155
    https://api.themoviedb.org/3/movie/
    Processing Record 326 of set2 | 11253
    https://api.themoviedb.org/3/movie/
    Processing Record 327 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 328 of set2 | 13813
    https://api.themoviedb.org/3/movie/
    Processing Record 329 of set2 | 10139
    https://api.themoviedb.org/3/movie/
    Processing Record 330 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 331 of set2 | 10673
    https://api.themoviedb.org/3/movie/
    Processing Record 332 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 333 of set2 | 11499
    https://api.themoviedb.org/3/movie/
    Processing Record 334 of set2 | 10139
    https://api.themoviedb.org/3/movie/
    Processing Record 335 of set2 | 8055
    https://api.themoviedb.org/3/movie/
    Processing Record 336 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 337 of set2 | 20722
    https://api.themoviedb.org/3/movie/
    Processing Record 338 of set2 | 149117
    https://api.themoviedb.org/3/movie/
    Processing Record 339 of set2 | 46343
    https://api.themoviedb.org/3/movie/
    Processing Record 340 of set2 | 13042
    https://api.themoviedb.org/3/movie/
    Processing Record 341 of set2 | 86118
    https://api.themoviedb.org/3/movie/
    Processing Record 342 of set2 | 200618
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 343 of set2 | 95608
    https://api.themoviedb.org/3/movie/
    Processing Record 344 of set2 | 9447
    https://api.themoviedb.org/3/movie/
    Processing Record 345 of set2 | 23764
    https://api.themoviedb.org/3/movie/
    Processing Record 346 of set2 | 155
    https://api.themoviedb.org/3/movie/
    Processing Record 347 of set2 | 1726
    https://api.themoviedb.org/3/movie/
    Processing Record 348 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 349 of set2 | 10673
    https://api.themoviedb.org/3/movie/
    Processing Record 350 of set2 | 8909
    https://api.themoviedb.org/3/movie/
    Processing Record 351 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 352 of set2 | 155
    https://api.themoviedb.org/3/movie/
    Processing Record 353 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 354 of set2 | 10673
    https://api.themoviedb.org/3/movie/
    Processing Record 355 of set2 | 8909
    https://api.themoviedb.org/3/movie/
    Processing Record 356 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 357 of set2 | 155
    https://api.themoviedb.org/3/movie/
    Processing Record 358 of set2 | 1726
    https://api.themoviedb.org/3/movie/
    Processing Record 359 of set2 | 4922
    https://api.themoviedb.org/3/movie/
    Processing Record 360 of set2 | 14359
    https://api.themoviedb.org/3/movie/
    Processing Record 361 of set2 | 11499
    https://api.themoviedb.org/3/movie/
    Processing Record 362 of set2 | 8055
    https://api.themoviedb.org/3/movie/
    Processing Record 363 of set2 | 12405
    https://api.themoviedb.org/3/movie/
    Processing Record 364 of set2 | 10183
    https://api.themoviedb.org/3/movie/
    Processing Record 365 of set2 | 10503
    https://api.themoviedb.org/3/movie/
    Processing Record 366 of set2 | 8321
    https://api.themoviedb.org/3/movie/
    Processing Record 367 of set2 | 10139
    https://api.themoviedb.org/3/movie/
    Processing Record 368 of set2 | 10673
    https://api.themoviedb.org/3/movie/
    Processing Record 369 of set2 | 18331
    https://api.themoviedb.org/3/movie/
    Processing Record 370 of set2 | 403011
    https://api.themoviedb.org/3/movie/
    Processing Record 371 of set2 | 522827
    https://api.themoviedb.org/3/movie/
    Processing Record 372 of set2 | 393640
    https://api.themoviedb.org/3/movie/
    Processing Record 373 of set2 | 371516
    https://api.themoviedb.org/3/movie/
    Processing Record 374 of set2 | 306048
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 375 of set2 | 9963
    https://api.themoviedb.org/3/movie/
    Processing Record 376 of set2 | 296273
    https://api.themoviedb.org/3/movie/
    Processing Record 377 of set2 | 162316
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 378 of set2 | 14836
    https://api.themoviedb.org/3/movie/
    Processing Record 379 of set2 | 10315
    https://api.themoviedb.org/3/movie/
    Processing Record 380 of set2 | 10198
    https://api.themoviedb.org/3/movie/
    Processing Record 381 of set2 | 26963
    https://api.themoviedb.org/3/movie/
    Processing Record 382 of set2 | 14160
    https://api.themoviedb.org/3/movie/
    Processing Record 383 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 384 of set2 | 8054
    https://api.themoviedb.org/3/movie/
    Processing Record 385 of set2 | 10197
    https://api.themoviedb.org/3/movie/
    Processing Record 386 of set2 | 10528
    https://api.themoviedb.org/3/movie/
    Processing Record 387 of set2 | 18320
    https://api.themoviedb.org/3/movie/
    Processing Record 388 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 389 of set2 | 767
    https://api.themoviedb.org/3/movie/
    Processing Record 390 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 391 of set2 | 16869
    https://api.themoviedb.org/3/movie/
    Processing Record 392 of set2 | 37903
    https://api.themoviedb.org/3/movie/
    Processing Record 393 of set2 | 29963
    https://api.themoviedb.org/3/movie/
    Processing Record 394 of set2 | 11156
    https://api.themoviedb.org/3/movie/
    Processing Record 395 of set2 | 8054
    https://api.themoviedb.org/3/movie/
    Processing Record 396 of set2 | 10197
    https://api.themoviedb.org/3/movie/
    Processing Record 397 of set2 | 18320
    https://api.themoviedb.org/3/movie/
    Processing Record 398 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 399 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 400 of set2 | 16869
    https://api.themoviedb.org/3/movie/
    Processing Record 401 of set2 | 25793
    https://api.themoviedb.org/3/movie/
    Processing Record 402 of set2 | 22947
    https://api.themoviedb.org/3/movie/
    Processing Record 403 of set2 | 26763
    https://api.themoviedb.org/3/movie/
    Processing Record 404 of set2 | 23128
    https://api.themoviedb.org/3/movie/
    Processing Record 405 of set2 | 18570
    https://api.themoviedb.org/3/movie/
    Processing Record 406 of set2 | 34576
    https://api.themoviedb.org/3/movie/
    Processing Record 407 of set2 | 55204
    https://api.themoviedb.org/3/movie/
    Processing Record 408 of set2 | 82248
    https://api.themoviedb.org/3/movie/
    Processing Record 409 of set2 | 245037
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 410 of set2 | 37098
    https://api.themoviedb.org/3/movie/
    Processing Record 411 of set2 | 154576
    https://api.themoviedb.org/3/movie/
    Processing Record 412 of set2 | 129427
    https://api.themoviedb.org/3/movie/
    Processing Record 413 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 414 of set2 | 17654
    https://api.themoviedb.org/3/movie/
    Processing Record 415 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 416 of set2 | 16869
    https://api.themoviedb.org/3/movie/
    Processing Record 417 of set2 | 25793
    https://api.themoviedb.org/3/movie/
    Processing Record 418 of set2 | 24424
    https://api.themoviedb.org/3/movie/
    Processing Record 419 of set2 | 28644
    https://api.themoviedb.org/3/movie/
    Processing Record 420 of set2 | 454610
    https://api.themoviedb.org/3/movie/
    Processing Record 421 of set2 | 25376
    https://api.themoviedb.org/3/movie/
    Processing Record 422 of set2 | 37903
    https://api.themoviedb.org/3/movie/
    Processing Record 423 of set2 | 8832
    https://api.themoviedb.org/3/movie/
    Processing Record 424 of set2 | 13475
    https://api.themoviedb.org/3/movie/
    Processing Record 425 of set2 | 18320
    https://api.themoviedb.org/3/movie/
    Processing Record 426 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 427 of set2 | 10315
    https://api.themoviedb.org/3/movie/
    Processing Record 428 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 429 of set2 | 10528
    https://api.themoviedb.org/3/movie/
    Processing Record 430 of set2 | 14160
    https://api.themoviedb.org/3/movie/
    Processing Record 431 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 432 of set2 | 22881
    https://api.themoviedb.org/3/movie/
    Processing Record 433 of set2 | 17654
    https://api.themoviedb.org/3/movie/
    Processing Record 434 of set2 | 24684
    https://api.themoviedb.org/3/movie/
    Processing Record 435 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 436 of set2 | 16869
    https://api.themoviedb.org/3/movie/
    Processing Record 437 of set2 | 25793
    https://api.themoviedb.org/3/movie/
    Processing Record 438 of set2 | 12573
    https://api.themoviedb.org/3/movie/
    Processing Record 439 of set2 | 14160
    https://api.themoviedb.org/3/movie/
    Processing Record 440 of set2 | 22947
    https://api.themoviedb.org/3/movie/
    Processing Record 441 of set2 | 37845
    https://api.themoviedb.org/3/movie/
    Processing Record 442 of set2 | 57091
    https://api.themoviedb.org/3/movie/
    Processing Record 443 of set2 | 62967
    https://api.themoviedb.org/3/movie/
    Processing Record 444 of set2 | 32389
    https://api.themoviedb.org/3/movie/
    Processing Record 445 of set2 | 14447
    https://api.themoviedb.org/3/movie/
    Processing Record 446 of set2 | 10591
    https://api.themoviedb.org/3/movie/
    Processing Record 447 of set2 | 161679
    https://api.themoviedb.org/3/movie/
    Processing Record 448 of set2 | 433618
    https://api.themoviedb.org/3/movie/
    Processing Record 449 of set2 | 56047
    https://api.themoviedb.org/3/movie/
    Processing Record 450 of set2 | 47798
    https://api.themoviedb.org/3/movie/
    Processing Record 451 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 452 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 453 of set2 | 16869
    https://api.themoviedb.org/3/movie/
    Processing Record 454 of set2 | 13475
    https://api.themoviedb.org/3/movie/
    Processing Record 455 of set2 | 14160
    https://api.themoviedb.org/3/movie/
    Processing Record 456 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 457 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 458 of set2 | 16869
    https://api.themoviedb.org/3/movie/
    Processing Record 459 of set2 | 13475
    https://api.themoviedb.org/3/movie/
    Processing Record 460 of set2 | 8373
    https://api.themoviedb.org/3/movie/
    Processing Record 461 of set2 | 19995
    https://api.themoviedb.org/3/movie/
    Processing Record 462 of set2 | 17654
    https://api.themoviedb.org/3/movie/
    Processing Record 463 of set2 | 13475
    https://api.themoviedb.org/3/movie/
    Processing Record 464 of set2 | 17654
    https://api.themoviedb.org/3/movie/
    Processing Record 465 of set2 | 24684
    https://api.themoviedb.org/3/movie/
    Processing Record 466 of set2 | 19833
    https://api.themoviedb.org/3/movie/
    Processing Record 467 of set2 | 25793
    https://api.themoviedb.org/3/movie/
    Processing Record 468 of set2 | 22947
    https://api.themoviedb.org/3/movie/
    Processing Record 469 of set2 | 12162
    https://api.themoviedb.org/3/movie/
    Processing Record 470 of set2 | 16869
    https://api.themoviedb.org/3/movie/
    Processing Record 471 of set2 | 28089
    https://api.themoviedb.org/3/movie/
    Processing Record 472 of set2 | 12573
    https://api.themoviedb.org/3/movie/
    Processing Record 473 of set2 | 14160
    https://api.themoviedb.org/3/movie/
    Processing Record 474 of set2 | 479518
    https://api.themoviedb.org/3/movie/
    Processing Record 475 of set2 | 256132
    https://api.themoviedb.org/3/movie/
    Processing Record 476 of set2 | 300302
    https://api.themoviedb.org/3/movie/
    Processing Record 477 of set2 | 393640
    https://api.themoviedb.org/3/movie/
    Processing Record 478 of set2 | 26058
    https://api.themoviedb.org/3/movie/
    Processing Record 479 of set2 | 373721
    https://api.themoviedb.org/3/movie/
    Processing Record 480 of set2 | 298545
    https://api.themoviedb.org/3/movie/
    Processing Record 481 of set2 | 10191
    https://api.themoviedb.org/3/movie/
    Processing Record 482 of set2 | 1491
    https://api.themoviedb.org/3/movie/
    Processing Record 483 of set2 | 10193
    https://api.themoviedb.org/3/movie/
    Processing Record 484 of set2 | 12155
    https://api.themoviedb.org/3/movie/
    Processing Record 485 of set2 | 12444
    https://api.themoviedb.org/3/movie/
    Processing Record 486 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 487 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 488 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 489 of set2 | 44214
    https://api.themoviedb.org/3/movie/
    Processing Record 490 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 491 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 492 of set2 | 37799
    https://api.themoviedb.org/3/movie/
    Processing Record 493 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 494 of set2 | 12155
    https://api.themoviedb.org/3/movie/
    Processing Record 495 of set2 | 370964
    https://api.themoviedb.org/3/movie/
    Processing Record 496 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 497 of set2 | 44638
    https://api.themoviedb.org/3/movie/
    Processing Record 498 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 499 of set2 | 44214
    https://api.themoviedb.org/3/movie/
    Processing Record 500 of set2 | 45317
    https://api.themoviedb.org/3/movie/
    Processing Record 501 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 502 of set2 | 37799
    https://api.themoviedb.org/3/movie/
    Processing Record 503 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 504 of set2 | 39452
    https://api.themoviedb.org/3/movie/
    Processing Record 505 of set2 | 40663
    https://api.themoviedb.org/3/movie/
    Processing Record 506 of set2 | 44639
    https://api.themoviedb.org/3/movie/
    Processing Record 507 of set2 | 39312
    https://api.themoviedb.org/3/movie/
    Processing Record 508 of set2 | 46689
    https://api.themoviedb.org/3/movie/
    Processing Record 509 of set2 | 128602
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 510 of set2 | 82421
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 511 of set2 | 113366
    https://api.themoviedb.org/3/movie/
    Processing Record 512 of set2 | 193504
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 513 of set2 | 245038
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 514 of set2 | 44214
    https://api.themoviedb.org/3/movie/
    Processing Record 515 of set2 | 45317
    https://api.themoviedb.org/3/movie/
    Processing Record 516 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 517 of set2 | 44115
    https://api.themoviedb.org/3/movie/
    Processing Record 518 of set2 | 37799
    https://api.themoviedb.org/3/movie/
    Processing Record 519 of set2 | 45958
    https://api.themoviedb.org/3/movie/
    Processing Record 520 of set2 | 38810
    https://api.themoviedb.org/3/movie/
    Processing Record 521 of set2 | 44716
    https://api.themoviedb.org/3/movie/
    Processing Record 522 of set2 | 46738
    https://api.themoviedb.org/3/movie/
    Processing Record 523 of set2 | 47904
    https://api.themoviedb.org/3/movie/
    Processing Record 524 of set2 | 46829
    https://api.themoviedb.org/3/movie/
    Processing Record 525 of set2 | 147773
    https://api.themoviedb.org/3/movie/
    Processing Record 526 of set2 | 7978
    https://api.themoviedb.org/3/movie/
    Processing Record 527 of set2 | 10191
    https://api.themoviedb.org/3/movie/
    Processing Record 528 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 529 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 530 of set2 | 44115
    https://api.themoviedb.org/3/movie/
    Processing Record 531 of set2 | 37799
    https://api.themoviedb.org/3/movie/
    Processing Record 532 of set2 | 44214
    https://api.themoviedb.org/3/movie/
    Processing Record 533 of set2 | 45317
    https://api.themoviedb.org/3/movie/
    Processing Record 534 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 535 of set2 | 39781
    https://api.themoviedb.org/3/movie/
    Processing Record 536 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 537 of set2 | 44115
    https://api.themoviedb.org/3/movie/
    Processing Record 538 of set2 | 37799
    https://api.themoviedb.org/3/movie/
    Processing Record 539 of set2 | 10193
    https://api.themoviedb.org/3/movie/
    Processing Record 540 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 541 of set2 | 39013
    https://api.themoviedb.org/3/movie/
    Processing Record 542 of set2 | 137
    https://api.themoviedb.org/3/movie/
    Processing Record 543 of set2 | 28118
    https://api.themoviedb.org/3/movie/
    Processing Record 544 of set2 | 159523
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 545 of set2 | 58515
    https://api.themoviedb.org/3/movie/
    Processing Record 546 of set2 | 30998
    https://api.themoviedb.org/3/movie/
    Processing Record 547 of set2 | 33408
    https://api.themoviedb.org/3/movie/
    Processing Record 548 of set2 | 195487
    https://api.themoviedb.org/3/movie/
    Processing Record 549 of set2 | 95468
    https://api.themoviedb.org/3/movie/
    Processing Record 550 of set2 | 159508
    https://api.themoviedb.org/3/movie/
    Processing Record 551 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 552 of set2 | 10193
    https://api.themoviedb.org/3/movie/
    Processing Record 553 of set2 | 20526
    https://api.themoviedb.org/3/movie/
    Processing Record 554 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 555 of set2 | 44048
    https://api.themoviedb.org/3/movie/
    Processing Record 556 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 557 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 558 of set2 | 27576
    https://api.themoviedb.org/3/movie/
    Processing Record 559 of set2 | 37799
    https://api.themoviedb.org/3/movie/
    Processing Record 560 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 561 of set2 | 12155
    https://api.themoviedb.org/3/movie/
    Processing Record 562 of set2 | 12444
    https://api.themoviedb.org/3/movie/
    Processing Record 563 of set2 | 44603
    https://api.themoviedb.org/3/movie/
    Processing Record 564 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 565 of set2 | 10138
    https://api.themoviedb.org/3/movie/
    Processing Record 566 of set2 | 44115
    https://api.themoviedb.org/3/movie/
    Processing Record 567 of set2 | 37799
    https://api.themoviedb.org/3/movie/
    Processing Record 568 of set2 | 10193
    https://api.themoviedb.org/3/movie/
    Processing Record 569 of set2 | 44264
    https://api.themoviedb.org/3/movie/
    Processing Record 570 of set2 | 39013
    https://api.themoviedb.org/3/movie/
    Processing Record 571 of set2 | 44009
    https://api.themoviedb.org/3/movie/
    Processing Record 572 of set2 | 45317
    https://api.themoviedb.org/3/movie/
    Processing Record 573 of set2 | 27205
    https://api.themoviedb.org/3/movie/
    Processing Record 574 of set2 | 39781
    https://api.themoviedb.org/3/movie/
    Processing Record 575 of set2 | 45269
    https://api.themoviedb.org/3/movie/
    Processing Record 576 of set2 | 187156
    https://api.themoviedb.org/3/movie/
    Processing Record 577 of set2 | 4539
    https://api.themoviedb.org/3/movie/
    Processing Record 578 of set2 | 403011
    https://api.themoviedb.org/3/movie/
    Processing Record 579 of set2 | 373895
    https://api.themoviedb.org/3/movie/
    Processing Record 580 of set2 | 104156
    https://api.themoviedb.org/3/movie/
    Processing Record 581 of set2 | 306048
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 582 of set2 | 277660
    https://api.themoviedb.org/3/movie/
    Processing Record 583 of set2 | 52264
    https://api.themoviedb.org/3/movie/
    Processing Record 584 of set2 | 63498
    https://api.themoviedb.org/3/movie/
    Processing Record 585 of set2 | 49444
    https://api.themoviedb.org/3/movie/
    Processing Record 586 of set2 | 417859
    https://api.themoviedb.org/3/movie/
    Processing Record 587 of set2 | 44896
    https://api.themoviedb.org/3/movie/
    Processing Record 588 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 589 of set2 | 12445
    https://api.themoviedb.org/3/movie/
    Processing Record 590 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 591 of set2 | 59436
    https://api.themoviedb.org/3/movie/
    Processing Record 592 of set2 | 57212
    https://api.themoviedb.org/3/movie/
    Processing Record 593 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 594 of set2 | 65754
    https://api.themoviedb.org/3/movie/
    Processing Record 595 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 596 of set2 | 8967
    https://api.themoviedb.org/3/movie/
    Processing Record 597 of set2 | 57212
    https://api.themoviedb.org/3/movie/
    Processing Record 598 of set2 | 61891
    https://api.themoviedb.org/3/movie/
    Processing Record 599 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 600 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 601 of set2 | 38684
    https://api.themoviedb.org/3/movie/
    Processing Record 602 of set2 | 80591
    https://api.themoviedb.org/3/movie/
    Processing Record 603 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 604 of set2 | 65057
    https://api.themoviedb.org/3/movie/
    Processing Record 605 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 606 of set2 | 59436
    https://api.themoviedb.org/3/movie/
    Processing Record 607 of set2 | 8967
    https://api.themoviedb.org/3/movie/
    Processing Record 608 of set2 | 74310
    https://api.themoviedb.org/3/movie/
    Processing Record 609 of set2 | 79042
    https://api.themoviedb.org/3/movie/
    Processing Record 610 of set2 | 83660
    https://api.themoviedb.org/3/movie/
    Processing Record 611 of set2 | 57276
    https://api.themoviedb.org/3/movie/
    Processing Record 612 of set2 | 82620
    https://api.themoviedb.org/3/movie/
    Processing Record 613 of set2 | 89194
    https://api.themoviedb.org/3/movie/
    Processing Record 614 of set2 | 103528
    https://api.themoviedb.org/3/movie/
    Processing Record 615 of set2 | 89196
    https://api.themoviedb.org/3/movie/
    Processing Record 616 of set2 | 19316
    https://api.themoviedb.org/3/movie/
    Processing Record 617 of set2 | 84346
    https://api.themoviedb.org/3/movie/
    Processing Record 618 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 619 of set2 | 65057
    https://api.themoviedb.org/3/movie/
    Processing Record 620 of set2 | 65754
    https://api.themoviedb.org/3/movie/
    Processing Record 621 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 622 of set2 | 60308
    https://api.themoviedb.org/3/movie/
    Processing Record 623 of set2 | 63310
    https://api.themoviedb.org/3/movie/
    Processing Record 624 of set2 | 72551
    https://api.themoviedb.org/3/movie/
    Processing Record 625 of set2 | 417643
    https://api.themoviedb.org/3/movie/
    Processing Record 626 of set2 | 78480
    https://api.themoviedb.org/3/movie/
    Processing Record 627 of set2 | 60243
    https://api.themoviedb.org/3/movie/
    Processing Record 628 of set2 | 73873
    https://api.themoviedb.org/3/movie/
    Processing Record 629 of set2 | 12445
    https://api.themoviedb.org/3/movie/
    Processing Record 630 of set2 | 71688
    https://api.themoviedb.org/3/movie/
    Processing Record 631 of set2 | 17578
    https://api.themoviedb.org/3/movie/
    Processing Record 632 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 633 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 634 of set2 | 49517
    https://api.themoviedb.org/3/movie/
    Processing Record 635 of set2 | 57212
    https://api.themoviedb.org/3/movie/
    Processing Record 636 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 637 of set2 | 65057
    https://api.themoviedb.org/3/movie/
    Processing Record 638 of set2 | 64685
    https://api.themoviedb.org/3/movie/
    Processing Record 639 of set2 | 50014
    https://api.themoviedb.org/3/movie/
    Processing Record 640 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 641 of set2 | 59436
    https://api.themoviedb.org/3/movie/
    Processing Record 642 of set2 | 60308
    https://api.themoviedb.org/3/movie/
    Processing Record 643 of set2 | 8967
    https://api.themoviedb.org/3/movie/
    Processing Record 644 of set2 | 57212
    https://api.themoviedb.org/3/movie/
    Processing Record 645 of set2 | 9563
    https://api.themoviedb.org/3/movie/
    Processing Record 646 of set2 | 86412
    https://api.themoviedb.org/3/movie/
    Processing Record 647 of set2 | 30636
    https://api.themoviedb.org/3/movie/
    Processing Record 648 of set2 | 91516
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 649 of set2 | 368940
    https://api.themoviedb.org/3/movie/
    Processing Record 650 of set2 | 99581
    https://api.themoviedb.org/3/movie/
    Processing Record 651 of set2 | 528765
    https://api.themoviedb.org/3/movie/
    Processing Record 652 of set2 | 465381
    https://api.themoviedb.org/3/movie/
    Processing Record 653 of set2 | 451925
    https://api.themoviedb.org/3/movie/
    Processing Record 654 of set2 | 92190
    https://api.themoviedb.org/3/movie/
    Processing Record 655 of set2 | 64690
    https://api.themoviedb.org/3/movie/
    Processing Record 656 of set2 | 65754
    https://api.themoviedb.org/3/movie/
    Processing Record 657 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 658 of set2 | 38356
    https://api.themoviedb.org/3/movie/
    Processing Record 659 of set2 | 57212
    https://api.themoviedb.org/3/movie/
    Processing Record 660 of set2 | 65754
    https://api.themoviedb.org/3/movie/
    Processing Record 661 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 662 of set2 | 60308
    https://api.themoviedb.org/3/movie/
    Processing Record 663 of set2 | 38356
    https://api.themoviedb.org/3/movie/
    Processing Record 664 of set2 | 57212
    https://api.themoviedb.org/3/movie/
    Processing Record 665 of set2 | 12445
    https://api.themoviedb.org/3/movie/
    Processing Record 666 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 667 of set2 | 39254
    https://api.themoviedb.org/3/movie/
    Processing Record 668 of set2 | 61791
    https://api.themoviedb.org/3/movie/
    Processing Record 669 of set2 | 38356
    https://api.themoviedb.org/3/movie/
    Processing Record 670 of set2 | 65057
    https://api.themoviedb.org/3/movie/
    Processing Record 671 of set2 | 44826
    https://api.themoviedb.org/3/movie/
    Processing Record 672 of set2 | 10316
    https://api.themoviedb.org/3/movie/
    Processing Record 673 of set2 | 60308
    https://api.themoviedb.org/3/movie/
    Processing Record 674 of set2 | 49517
    https://api.themoviedb.org/3/movie/
    Processing Record 675 of set2 | 74643
    https://api.themoviedb.org/3/movie/
    Processing Record 676 of set2 | 55721
    https://api.themoviedb.org/3/movie/
    Processing Record 677 of set2 | 50839
    https://api.themoviedb.org/3/movie/
    Processing Record 678 of set2 | 59436
    https://api.themoviedb.org/3/movie/
    Processing Record 679 of set2 | 60243
    https://api.themoviedb.org/3/movie/
    Processing Record 680 of set2 | 26132
    https://api.themoviedb.org/3/movie/
    Processing Record 681 of set2 | 256521
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 682 of set2 | 566838
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 683 of set2 | 43939
    https://api.themoviedb.org/3/movie/
    Processing Record 684 of set2 | 304533
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 685 of set2 | 248829
    https://api.themoviedb.org/3/movie/
    Processing Record 686 of set2 | 373721
    https://api.themoviedb.org/3/movie/
    Processing Record 687 of set2 | 51828
    https://api.themoviedb.org/3/movie/
    Processing Record 688 of set2 | 62177
    https://api.themoviedb.org/3/movie/
    Processing Record 689 of set2 | 62214
    https://api.themoviedb.org/3/movie/
    Processing Record 690 of set2 | 77174
    https://api.themoviedb.org/3/movie/
    Processing Record 691 of set2 | 72197
    https://api.themoviedb.org/3/movie/
    Processing Record 692 of set2 | 82690
    https://api.themoviedb.org/3/movie/
    Processing Record 693 of set2 | 96724
    https://api.themoviedb.org/3/movie/
    Processing Record 694 of set2 | 68718
    https://api.themoviedb.org/3/movie/
    Processing Record 695 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 696 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 697 of set2 | 37724
    https://api.themoviedb.org/3/movie/
    Processing Record 698 of set2 | 96724
    https://api.themoviedb.org/3/movie/
    Processing Record 699 of set2 | 82695
    https://api.themoviedb.org/3/movie/
    Processing Record 700 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 701 of set2 | 62764
    https://api.themoviedb.org/3/movie/
    Processing Record 702 of set2 | 58595
    https://api.themoviedb.org/3/movie/
    Processing Record 703 of set2 | 86837
    https://api.themoviedb.org/3/movie/
    Processing Record 704 of set2 | 84175
    https://api.themoviedb.org/3/movie/
    Processing Record 705 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 706 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 707 of set2 | 82693
    https://api.themoviedb.org/3/movie/
    Processing Record 708 of set2 | 84170
    https://api.themoviedb.org/3/movie/
    Processing Record 709 of set2 | 127918
    https://api.themoviedb.org/3/movie/
    Processing Record 710 of set2 | 84286
    https://api.themoviedb.org/3/movie/
    Processing Record 711 of set2 | 84288
    https://api.themoviedb.org/3/movie/
    Processing Record 712 of set2 | 84334
    https://api.themoviedb.org/3/movie/
    Processing Record 713 of set2 | 30671
    https://api.themoviedb.org/3/movie/
    Processing Record 714 of set2 | 137651
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 715 of set2 | 137652
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 716 of set2 | 80291
    https://api.themoviedb.org/3/movie/
    Processing Record 717 of set2 | 278
    https://api.themoviedb.org/3/movie/
    Processing Record 718 of set2 | 68734
    https://api.themoviedb.org/3/movie/
    Processing Record 719 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 720 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 721 of set2 | 82693
    https://api.themoviedb.org/3/movie/
    Processing Record 722 of set2 | 97630
    https://api.themoviedb.org/3/movie/
    Processing Record 723 of set2 | 86837
    https://api.themoviedb.org/3/movie/
    Processing Record 724 of set2 | 70667
    https://api.themoviedb.org/3/movie/
    Processing Record 725 of set2 | 646
    https://api.themoviedb.org/3/movie/
    Processing Record 726 of set2 | 88273
    https://api.themoviedb.org/3/movie/
    Processing Record 727 of set2 | 98205
    https://api.themoviedb.org/3/movie/
    Processing Record 728 of set2 | 112336
    https://api.themoviedb.org/3/movie/
    Processing Record 729 of set2 | 49051
    https://api.themoviedb.org/3/movie/
    Processing Record 730 of set2 | 82695
    https://api.themoviedb.org/3/movie/
    Processing Record 731 of set2 | 96724
    https://api.themoviedb.org/3/movie/
    Processing Record 732 of set2 | 68734
    https://api.themoviedb.org/3/movie/
    Processing Record 733 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 734 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 735 of set2 | 37724
    https://api.themoviedb.org/3/movie/
    Processing Record 736 of set2 | 86837
    https://api.themoviedb.org/3/movie/
    Processing Record 737 of set2 | 68734
    https://api.themoviedb.org/3/movie/
    Processing Record 738 of set2 | 84175
    https://api.themoviedb.org/3/movie/
    Processing Record 739 of set2 | 68718
    https://api.themoviedb.org/3/movie/
    Processing Record 740 of set2 | 82695
    https://api.themoviedb.org/3/movie/
    Processing Record 741 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 742 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 743 of set2 | 82693
    https://api.themoviedb.org/3/movie/
    Processing Record 744 of set2 | 97630
    https://api.themoviedb.org/3/movie/
    Processing Record 745 of set2 | 96724
    https://api.themoviedb.org/3/movie/
    Processing Record 746 of set2 | 49051
    https://api.themoviedb.org/3/movie/
    Processing Record 747 of set2 | 82695
    https://api.themoviedb.org/3/movie/
    Processing Record 748 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 749 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 750 of set2 | 157301
    https://api.themoviedb.org/3/movie/
    Processing Record 751 of set2 | 142563
    https://api.themoviedb.org/3/movie/
    Processing Record 752 of set2 | 24940
    https://api.themoviedb.org/3/movie/
    Processing Record 753 of set2 | 116440
    https://api.themoviedb.org/3/movie/
    Processing Record 754 of set2 | 140420
    https://api.themoviedb.org/3/movie/
    Processing Record 755 of set2 | 146891
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 756 of set2 | 146892
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 757 of set2 | 157289
    https://api.themoviedb.org/3/movie/
    Processing Record 758 of set2 | 325348
    https://api.themoviedb.org/3/movie/
    Processing Record 759 of set2 | 68734
    https://api.themoviedb.org/3/movie/
    Processing Record 760 of set2 | 68718
    https://api.themoviedb.org/3/movie/
    Processing Record 761 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 762 of set2 | 37724
    https://api.themoviedb.org/3/movie/
    Processing Record 763 of set2 | 97630
    https://api.themoviedb.org/3/movie/
    Processing Record 764 of set2 | 68734
    https://api.themoviedb.org/3/movie/
    Processing Record 765 of set2 | 82695
    https://api.themoviedb.org/3/movie/
    Processing Record 766 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 767 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 768 of set2 | 37724
    https://api.themoviedb.org/3/movie/
    Processing Record 769 of set2 | 49051
    https://api.themoviedb.org/3/movie/
    Processing Record 770 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 771 of set2 | 24428
    https://api.themoviedb.org/3/movie/
    Processing Record 772 of set2 | 70981
    https://api.themoviedb.org/3/movie/
    Processing Record 773 of set2 | 58595
    https://api.themoviedb.org/3/movie/
    Processing Record 774 of set2 | 68734
    https://api.themoviedb.org/3/movie/
    Processing Record 775 of set2 | 84175
    https://api.themoviedb.org/3/movie/
    Processing Record 776 of set2 | 87827
    https://api.themoviedb.org/3/movie/
    Processing Record 777 of set2 | 72976
    https://api.themoviedb.org/3/movie/
    Processing Record 778 of set2 | 82693
    https://api.themoviedb.org/3/movie/
    Processing Record 779 of set2 | 86837
    https://api.themoviedb.org/3/movie/
    Processing Record 780 of set2 | 68718
    https://api.themoviedb.org/3/movie/
    Processing Record 781 of set2 | 87502
    https://api.themoviedb.org/3/movie/
    Processing Record 782 of set2 | 83666
    https://api.themoviedb.org/3/movie/
    Processing Record 783 of set2 | 97630
    https://api.themoviedb.org/3/movie/
    Processing Record 784 of set2 | 541295
    https://api.themoviedb.org/3/movie/
    Processing Record 785 of set2 | 515632
    https://api.themoviedb.org/3/movie/
    Processing Record 786 of set2 | 299947
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 787 of set2 | 533864
    https://api.themoviedb.org/3/movie/
    Processing Record 788 of set2 | 9963
    https://api.themoviedb.org/3/movie/
    Processing Record 789 of set2 | 493597
    https://api.themoviedb.org/3/movie/
    Processing Record 790 of set2 | 373721
    https://api.themoviedb.org/3/movie/
    Processing Record 791 of set2 | 552691
    https://api.themoviedb.org/3/movie/
    Processing Record 792 of set2 | 49519
    https://api.themoviedb.org/3/movie/
    Processing Record 793 of set2 | 93456
    https://api.themoviedb.org/3/movie/
    Processing Record 794 of set2 | 126319
    https://api.themoviedb.org/3/movie/
    Processing Record 795 of set2 | 109445
    https://api.themoviedb.org/3/movie/
    Processing Record 796 of set2 | 149870
    https://api.themoviedb.org/3/movie/
    Processing Record 797 of set2 | 44865
    https://api.themoviedb.org/3/movie/
    Processing Record 798 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 799 of set2 | 86829
    https://api.themoviedb.org/3/movie/
    Processing Record 800 of set2 | 129670
    https://api.themoviedb.org/3/movie/
    Processing Record 801 of set2 | 146233
    https://api.themoviedb.org/3/movie/
    Processing Record 802 of set2 | 168672
    https://api.themoviedb.org/3/movie/
    Processing Record 803 of set2 | 44865
    https://api.themoviedb.org/3/movie/
    Processing Record 804 of set2 | 64682
    https://api.themoviedb.org/3/movie/
    Processing Record 805 of set2 | 111473
    https://api.themoviedb.org/3/movie/
    Processing Record 806 of set2 | 76203
    https://api.themoviedb.org/3/movie/
    Processing Record 807 of set2 | 168672
    https://api.themoviedb.org/3/movie/
    Processing Record 808 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 809 of set2 | 129670
    https://api.themoviedb.org/3/movie/
    Processing Record 810 of set2 | 76203
    https://api.themoviedb.org/3/movie/
    Processing Record 811 of set2 | 106646
    https://api.themoviedb.org/3/movie/
    Processing Record 812 of set2 | 123678
    https://api.themoviedb.org/3/movie/
    Processing Record 813 of set2 | 159002
    https://api.themoviedb.org/3/movie/
    Processing Record 814 of set2 | 159004
    https://api.themoviedb.org/3/movie/
    Processing Record 815 of set2 | 401246
    https://api.themoviedb.org/3/movie/
    Processing Record 816 of set2 | 159014
    https://api.themoviedb.org/3/movie/
    Processing Record 817 of set2 | 249714
    https://api.themoviedb.org/3/movie/
    Processing Record 818 of set2 | 249719
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 819 of set2 | 249721
    https://api.themoviedb.org/3/movie/
    Processing Record 820 of set2 | 443313
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 821 of set2 | 249726
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 822 of set2 | 168672
    https://api.themoviedb.org/3/movie/
    Processing Record 823 of set2 | 109424
    https://api.themoviedb.org/3/movie/
    Processing Record 824 of set2 | 152532
    https://api.themoviedb.org/3/movie/
    Processing Record 825 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 826 of set2 | 76203
    https://api.themoviedb.org/3/movie/
    Processing Record 827 of set2 | 137182
    https://api.themoviedb.org/3/movie/
    Processing Record 828 of set2 | 247794
    https://api.themoviedb.org/3/movie/
    Processing Record 829 of set2 | 371645
    https://api.themoviedb.org/3/movie/
    Processing Record 830 of set2 | 186997
    https://api.themoviedb.org/3/movie/
    Processing Record 831 of set2 | 68178
    https://api.themoviedb.org/3/movie/
    Processing Record 832 of set2 | 152532
    https://api.themoviedb.org/3/movie/
    Processing Record 833 of set2 | 208134
    https://api.themoviedb.org/3/movie/
    Processing Record 834 of set2 | 57201
    https://api.themoviedb.org/3/movie/
    Processing Record 835 of set2 | 203833
    https://api.themoviedb.org/3/movie/
    Processing Record 836 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 837 of set2 | 152601
    https://api.themoviedb.org/3/movie/
    Processing Record 838 of set2 | 205220
    https://api.themoviedb.org/3/movie/
    Processing Record 839 of set2 | 140823
    https://api.themoviedb.org/3/movie/
    Processing Record 840 of set2 | 168672
    https://api.themoviedb.org/3/movie/
    Processing Record 841 of set2 | 109424
    https://api.themoviedb.org/3/movie/
    Processing Record 842 of set2 | 152532
    https://api.themoviedb.org/3/movie/
    Processing Record 843 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 844 of set2 | 152601
    https://api.themoviedb.org/3/movie/
    Processing Record 845 of set2 | 129670
    https://api.themoviedb.org/3/movie/
    Processing Record 846 of set2 | 205220
    https://api.themoviedb.org/3/movie/
    Processing Record 847 of set2 | 76203
    https://api.themoviedb.org/3/movie/
    Processing Record 848 of set2 | 106646
    https://api.themoviedb.org/3/movie/
    Processing Record 849 of set2 | 168672
    https://api.themoviedb.org/3/movie/
    Processing Record 850 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 851 of set2 | 64682
    https://api.themoviedb.org/3/movie/
    Processing Record 852 of set2 | 152601
    https://api.themoviedb.org/3/movie/
    Processing Record 853 of set2 | 76203
    https://api.themoviedb.org/3/movie/
    Processing Record 854 of set2 | 436494
    https://api.themoviedb.org/3/movie/
    Processing Record 855 of set2 | 234567
    https://api.themoviedb.org/3/movie/
    Processing Record 856 of set2 | 234862
    https://api.themoviedb.org/3/movie/
    Processing Record 857 of set2 | 323665
    https://api.themoviedb.org/3/movie/
    Processing Record 858 of set2 | 152581
    https://api.themoviedb.org/3/movie/
    Processing Record 859 of set2 | 222796
    https://api.themoviedb.org/3/movie/
    Processing Record 860 of set2 | 249699
    https://api.themoviedb.org/3/movie/
    Processing Record 861 of set2 | 200942
    https://api.themoviedb.org/3/movie/
    Processing Record 862 of set2 | 152747
    https://api.themoviedb.org/3/movie/
    Processing Record 863 of set2 | 109424
    https://api.themoviedb.org/3/movie/
    Processing Record 864 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 865 of set2 | 57158
    https://api.themoviedb.org/3/movie/
    Processing Record 866 of set2 | 193756
    https://api.themoviedb.org/3/movie/
    Processing Record 867 of set2 | 109424
    https://api.themoviedb.org/3/movie/
    Processing Record 868 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 869 of set2 | 57158
    https://api.themoviedb.org/3/movie/
    Processing Record 870 of set2 | 86829
    https://api.themoviedb.org/3/movie/
    Processing Record 871 of set2 | 193756
    https://api.themoviedb.org/3/movie/
    Processing Record 872 of set2 | 49047
    https://api.themoviedb.org/3/movie/
    Processing Record 873 of set2 | 57158
    https://api.themoviedb.org/3/movie/
    Processing Record 874 of set2 | 68721
    https://api.themoviedb.org/3/movie/
    Processing Record 875 of set2 | 57201
    https://api.themoviedb.org/3/movie/
    Processing Record 876 of set2 | 54138
    https://api.themoviedb.org/3/movie/
    Processing Record 877 of set2 | 132344
    https://api.themoviedb.org/3/movie/
    Processing Record 878 of set2 | 109424
    https://api.themoviedb.org/3/movie/
    Processing Record 879 of set2 | 205220
    https://api.themoviedb.org/3/movie/
    Processing Record 880 of set2 | 76203
    https://api.themoviedb.org/3/movie/
    Processing Record 881 of set2 | 106646
    https://api.themoviedb.org/3/movie/
    Processing Record 882 of set2 | 168672
    https://api.themoviedb.org/3/movie/
    Processing Record 883 of set2 | 160588
    https://api.themoviedb.org/3/movie/
    Processing Record 884 of set2 | 152532
    https://api.themoviedb.org/3/movie/
    Processing Record 885 of set2 | 152601
    https://api.themoviedb.org/3/movie/
    Processing Record 886 of set2 | 129670
    https://api.themoviedb.org/3/movie/
    Processing Record 887 of set2 | 456881
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 888 of set2 | 162637
    https://api.themoviedb.org/3/movie/
    Processing Record 889 of set2 | 459800
    https://api.themoviedb.org/3/movie/
    Processing Record 890 of set2 | 339410
    https://api.themoviedb.org/3/movie/
    Processing Record 891 of set2 | 177572
    https://api.themoviedb.org/3/movie/
    Processing Record 892 of set2 | 170687
    https://api.themoviedb.org/3/movie/
    Processing Record 893 of set2 | 82702
    https://api.themoviedb.org/3/movie/
    Processing Record 894 of set2 | 110416
    https://api.themoviedb.org/3/movie/
    Processing Record 895 of set2 | 149871
    https://api.themoviedb.org/3/movie/
    Processing Record 896 of set2 | 194662
    https://api.themoviedb.org/3/movie/
    Processing Record 897 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 898 of set2 | 209274
    https://api.themoviedb.org/3/movie/
    Processing Record 899 of set2 | 245700
    https://api.themoviedb.org/3/movie/
    Processing Record 900 of set2 | 227306
    https://api.themoviedb.org/3/movie/
    Processing Record 901 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 902 of set2 | 171274
    https://api.themoviedb.org/3/movie/
    Processing Record 903 of set2 | 224141
    https://api.themoviedb.org/3/movie/
    Processing Record 904 of set2 | 102651
    https://api.themoviedb.org/3/movie/
    Processing Record 905 of set2 | 245700
    https://api.themoviedb.org/3/movie/
    Processing Record 906 of set2 | 194662
    https://api.themoviedb.org/3/movie/
    Processing Record 907 of set2 | 85350
    https://api.themoviedb.org/3/movie/
    Processing Record 908 of set2 | 87492
    https://api.themoviedb.org/3/movie/
    Processing Record 909 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 910 of set2 | 205596
    https://api.themoviedb.org/3/movie/
    Processing Record 911 of set2 | 293310
    https://api.themoviedb.org/3/movie/
    Processing Record 912 of set2 | 169607
    https://api.themoviedb.org/3/movie/
    Processing Record 913 of set2 | 250761
    https://api.themoviedb.org/3/movie/
    Processing Record 914 of set2 | 23620
    https://api.themoviedb.org/3/movie/
    Processing Record 915 of set2 | 263614
    https://api.themoviedb.org/3/movie/
    Processing Record 916 of set2 | 248808
    https://api.themoviedb.org/3/movie/
    Processing Record 917 of set2 | 300176
    https://api.themoviedb.org/3/movie/
    Processing Record 918 of set2 | 274805
    https://api.themoviedb.org/3/movie/
    Processing Record 919 of set2 | 259520
    https://api.themoviedb.org/3/movie/
    Processing Record 920 of set2 | 190859
    https://api.themoviedb.org/3/movie/
    Processing Record 921 of set2 | 85350
    https://api.themoviedb.org/3/movie/
    Processing Record 922 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 923 of set2 | 205596
    https://api.themoviedb.org/3/movie/
    Processing Record 924 of set2 | 244786
    https://api.themoviedb.org/3/movie/
    Processing Record 925 of set2 | 209274
    https://api.themoviedb.org/3/movie/
    Processing Record 926 of set2 | 14372
    https://api.themoviedb.org/3/movie/
    Processing Record 927 of set2 | 238628
    https://api.themoviedb.org/3/movie/
    Processing Record 928 of set2 | 265228
    https://api.themoviedb.org/3/movie/
    Processing Record 929 of set2 | 265195
    https://api.themoviedb.org/3/movie/
    Processing Record 930 of set2 | 87492
    https://api.themoviedb.org/3/movie/
    Processing Record 931 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 932 of set2 | 118340
    https://api.themoviedb.org/3/movie/
    Processing Record 933 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 934 of set2 | 205596
    https://api.themoviedb.org/3/movie/
    Processing Record 935 of set2 | 157336
    https://api.themoviedb.org/3/movie/
    Processing Record 936 of set2 | 245700
    https://api.themoviedb.org/3/movie/
    Processing Record 937 of set2 | 266856
    https://api.themoviedb.org/3/movie/
    Processing Record 938 of set2 | 190859
    https://api.themoviedb.org/3/movie/
    Processing Record 939 of set2 | 194662
    https://api.themoviedb.org/3/movie/
    Processing Record 940 of set2 | 85350
    https://api.themoviedb.org/3/movie/
    Processing Record 941 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 942 of set2 | 205596
    https://api.themoviedb.org/3/movie/
    Processing Record 943 of set2 | 273895
    https://api.themoviedb.org/3/movie/
    Processing Record 944 of set2 | 266856
    https://api.themoviedb.org/3/movie/
    Processing Record 945 of set2 | 244786
    https://api.themoviedb.org/3/movie/
    Processing Record 946 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 947 of set2 | 205596
    https://api.themoviedb.org/3/movie/
    Processing Record 948 of set2 | 157336
    https://api.themoviedb.org/3/movie/
    Processing Record 949 of set2 | 224141
    https://api.themoviedb.org/3/movie/
    Processing Record 950 of set2 | 245700
    https://api.themoviedb.org/3/movie/
    Processing Record 951 of set2 | 307695
    https://api.themoviedb.org/3/movie/
    Processing Record 952 of set2 | 254273
    https://api.themoviedb.org/3/movie/
    Processing Record 953 of set2 | 293299
    https://api.themoviedb.org/3/movie/
    Processing Record 954 of set2 | 289024
    https://api.themoviedb.org/3/movie/
    Processing Record 955 of set2 | 289280
    https://api.themoviedb.org/3/movie/
    Processing Record 956 of set2 | 550826
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 957 of set2 | 307686
    https://api.themoviedb.org/3/movie/
    Processing Record 958 of set2 | 307692
    https://api.themoviedb.org/3/movie/
    Processing Record 959 of set2 | 220809
    https://api.themoviedb.org/3/movie/
    Processing Record 960 of set2 | 190859
    https://api.themoviedb.org/3/movie/
    Processing Record 961 of set2 | 194662
    https://api.themoviedb.org/3/movie/
    Processing Record 962 of set2 | 122917
    https://api.themoviedb.org/3/movie/
    Processing Record 963 of set2 | 157336
    https://api.themoviedb.org/3/movie/
    Processing Record 964 of set2 | 227306
    https://api.themoviedb.org/3/movie/
    Processing Record 965 of set2 | 190859
    https://api.themoviedb.org/3/movie/
    Processing Record 966 of set2 | 194662
    https://api.themoviedb.org/3/movie/
    Processing Record 967 of set2 | 157336
    https://api.themoviedb.org/3/movie/
    Processing Record 968 of set2 | 227306
    https://api.themoviedb.org/3/movie/
    Processing Record 969 of set2 | 244786
    https://api.themoviedb.org/3/movie/
    Processing Record 970 of set2 | 100402
    https://api.themoviedb.org/3/movie/
    Processing Record 971 of set2 | 119450
    https://api.themoviedb.org/3/movie/
    Processing Record 972 of set2 | 118340
    https://api.themoviedb.org/3/movie/
    Processing Record 973 of set2 | 157336
    https://api.themoviedb.org/3/movie/
    Processing Record 974 of set2 | 127585
    https://api.themoviedb.org/3/movie/
    Processing Record 975 of set2 | 190859
    https://api.themoviedb.org/3/movie/
    Processing Record 976 of set2 | 205596
    https://api.themoviedb.org/3/movie/
    Processing Record 977 of set2 | 171274
    https://api.themoviedb.org/3/movie/
    Processing Record 978 of set2 | 266856
    https://api.themoviedb.org/3/movie/
    Processing Record 979 of set2 | 244786
    https://api.themoviedb.org/3/movie/
    Processing Record 980 of set2 | 194662
    https://api.themoviedb.org/3/movie/
    Processing Record 981 of set2 | 85350
    https://api.themoviedb.org/3/movie/
    Processing Record 982 of set2 | 87492
    https://api.themoviedb.org/3/movie/
    Processing Record 983 of set2 | 120467
    https://api.themoviedb.org/3/movie/
    Processing Record 984 of set2 | 242582
    https://api.themoviedb.org/3/movie/
    Processing Record 985 of set2 | 91367
    https://api.themoviedb.org/3/movie/
    Processing Record 986 of set2 | 452630
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 987 of set2 | 371516
    https://api.themoviedb.org/3/movie/
    Processing Record 988 of set2 | 42299
    https://api.themoviedb.org/3/movie/
    Processing Record 989 of set2 | 10477
    https://api.themoviedb.org/3/movie/
    Processing Record 990 of set2 | 531352
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 991 of set2 | 373721
    https://api.themoviedb.org/3/movie/
    Processing Record 992 of set2 | 82673
    https://api.themoviedb.org/3/movie/
    Processing Record 993 of set2 | 291270
    https://api.themoviedb.org/3/movie/
    Processing Record 994 of set2 | 223706
    https://api.themoviedb.org/3/movie/
    Processing Record 995 of set2 | 150540
    https://api.themoviedb.org/3/movie/
    Processing Record 996 of set2 | 263109
    https://api.themoviedb.org/3/movie/
    Processing Record 997 of set2 | 242828
    https://api.themoviedb.org/3/movie/
    Processing Record 998 of set2 | 258480
    https://api.themoviedb.org/3/movie/
    Processing Record 999 of set2 | 273248
    https://api.themoviedb.org/3/movie/
    Processing Record 1000 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1001 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1002 of set2 | 273481
    https://api.themoviedb.org/3/movie/
    Processing Record 1003 of set2 | 258480
    https://api.themoviedb.org/3/movie/
    Processing Record 1004 of set2 | 150689
    https://api.themoviedb.org/3/movie/
    Processing Record 1005 of set2 | 306819
    https://api.themoviedb.org/3/movie/
    Processing Record 1006 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1007 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1008 of set2 | 318846
    https://api.themoviedb.org/3/movie/
    Processing Record 1009 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1010 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1011 of set2 | 264644
    https://api.themoviedb.org/3/movie/
    Processing Record 1012 of set2 | 314365
    https://api.themoviedb.org/3/movie/
    Processing Record 1013 of set2 | 331781
    https://api.themoviedb.org/3/movie/
    Processing Record 1014 of set2 | 317952
    https://api.themoviedb.org/3/movie/
    Processing Record 1015 of set2 | 267480
    https://api.themoviedb.org/3/movie/
    Processing Record 1016 of set2 | 318044
    https://api.themoviedb.org/3/movie/
    Processing Record 1017 of set2 | 355020
    https://api.themoviedb.org/3/movie/
    Processing Record 1018 of set2 | 365447
    https://api.themoviedb.org/3/movie/
    Processing Record 1019 of set2 | 369362
    https://api.themoviedb.org/3/movie/
    Processing Record 1020 of set2 | 369363
    https://api.themoviedb.org/3/movie/
    <class 'IndexError'>
    list index out of range
    Processing Record 1021 of set2 | 369364
    https://api.themoviedb.org/3/movie/
    Processing Record 1022 of set2 | 369366
    https://api.themoviedb.org/3/movie/
    Processing Record 1023 of set2 | 318846
    https://api.themoviedb.org/3/movie/
    Processing Record 1024 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1025 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1026 of set2 | 314365
    https://api.themoviedb.org/3/movie/
    Processing Record 1027 of set2 | 140607
    https://api.themoviedb.org/3/movie/
    Processing Record 1028 of set2 | 336808
    https://api.themoviedb.org/3/movie/
    Processing Record 1029 of set2 | 336804
    https://api.themoviedb.org/3/movie/
    Processing Record 1030 of set2 | 336050
    https://api.themoviedb.org/3/movie/
    Processing Record 1031 of set2 | 287628
    https://api.themoviedb.org/3/movie/
    Processing Record 1032 of set2 | 475132
    https://api.themoviedb.org/3/movie/
    Processing Record 1033 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1034 of set2 | 145247
    https://api.themoviedb.org/3/movie/
    Processing Record 1035 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1036 of set2 | 296098
    https://api.themoviedb.org/3/movie/
    Processing Record 1037 of set2 | 258480
    https://api.themoviedb.org/3/movie/
    Processing Record 1038 of set2 | 273248
    https://api.themoviedb.org/3/movie/
    Processing Record 1039 of set2 | 273481
    https://api.themoviedb.org/3/movie/
    Processing Record 1040 of set2 | 140607
    https://api.themoviedb.org/3/movie/
    Processing Record 1041 of set2 | 547766
    https://api.themoviedb.org/3/movie/
    Processing Record 1042 of set2 | 318846
    https://api.themoviedb.org/3/movie/
    Processing Record 1043 of set2 | 296098
    https://api.themoviedb.org/3/movie/
    Processing Record 1044 of set2 | 167073
    https://api.themoviedb.org/3/movie/
    Processing Record 1045 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1046 of set2 | 286217
    https://api.themoviedb.org/3/movie/
    Processing Record 1047 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1048 of set2 | 264644
    https://api.themoviedb.org/3/movie/
    Processing Record 1049 of set2 | 314365
    https://api.themoviedb.org/3/movie/
    Processing Record 1050 of set2 | 296098
    https://api.themoviedb.org/3/movie/
    Processing Record 1051 of set2 | 306819
    https://api.themoviedb.org/3/movie/
    Processing Record 1052 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1053 of set2 | 286217
    https://api.themoviedb.org/3/movie/
    Processing Record 1054 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1055 of set2 | 351981
    https://api.themoviedb.org/3/movie/
    Processing Record 1056 of set2 | 359549
    https://api.themoviedb.org/3/movie/
    Processing Record 1057 of set2 | 345637
    https://api.themoviedb.org/3/movie/
    Processing Record 1058 of set2 | 329063
    https://api.themoviedb.org/3/movie/
    Processing Record 1059 of set2 | 303867
    https://api.themoviedb.org/3/movie/
    Processing Record 1060 of set2 | 348396
    https://api.themoviedb.org/3/movie/
    Processing Record 1061 of set2 | 51828
    https://api.themoviedb.org/3/movie/
    Processing Record 1062 of set2 | 366736
    https://api.themoviedb.org/3/movie/
    Processing Record 1063 of set2 | 369373
    https://api.themoviedb.org/3/movie/
    Processing Record 1064 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1065 of set2 | 286217
    https://api.themoviedb.org/3/movie/
    Processing Record 1066 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1067 of set2 | 273481
    https://api.themoviedb.org/3/movie/
    Processing Record 1068 of set2 | 140607
    https://api.themoviedb.org/3/movie/
    Processing Record 1069 of set2 | 296098
    https://api.themoviedb.org/3/movie/
    Processing Record 1070 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1071 of set2 | 286217
    https://api.themoviedb.org/3/movie/
    Processing Record 1072 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1073 of set2 | 140607
    https://api.themoviedb.org/3/movie/
    Processing Record 1074 of set2 | 264660
    https://api.themoviedb.org/3/movie/
    Processing Record 1075 of set2 | 76341
    https://api.themoviedb.org/3/movie/
    Processing Record 1076 of set2 | 286217
    https://api.themoviedb.org/3/movie/
    Processing Record 1077 of set2 | 281957
    https://api.themoviedb.org/3/movie/
    Processing Record 1078 of set2 | 140607
    https://api.themoviedb.org/3/movie/
    Processing Record 1079 of set2 | 318846
    https://api.themoviedb.org/3/movie/
    Processing Record 1080 of set2 | 167073
    https://api.themoviedb.org/3/movie/
    Processing Record 1081 of set2 | 258480
    https://api.themoviedb.org/3/movie/
    Processing Record 1082 of set2 | 286217
    https://api.themoviedb.org/3/movie/
    Processing Record 1083 of set2 | 264644
    https://api.themoviedb.org/3/movie/
    Processing Record 1084 of set2 | 296098
    https://api.themoviedb.org/3/movie/
    Processing Record 1085 of set2 | 264660
    https://api.themoviedb.org/3/movie/
    Processing Record 1086 of set2 | 150540
    https://api.themoviedb.org/3/movie/
    Processing Record 1087 of set2 | 314365
    https://api.themoviedb.org/3/movie/
    Processing Record 1088 of set2 | 277216
    https://api.themoviedb.org/3/movie/
    Processing Record 1089 of set2 | 398738
    https://api.themoviedb.org/3/movie/
    Processing Record 1090 of set2 | 9469
    https://api.themoviedb.org/3/movie/
    ------------------------------ 
     End of Data Retrieval 
    ------------------------------
    251
    


```python
movies_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Movie</th>
      <th>Release Date</th>
      <th>Budget</th>
      <th>Revenue</th>
      <th>Genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Terrence Howard's Fright Club</td>
      <td>2018-05-24</td>
      <td>0</td>
      <td>0</td>
      <td>Comedy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>I Am Heath Ledger</td>
      <td>2017-04-23</td>
      <td>0</td>
      <td>0</td>
      <td>Documentary</td>
    </tr>
    <tr>
      <th>2</th>
      <td>I'm Still Here</td>
      <td>2010-09-10</td>
      <td>0</td>
      <td>0</td>
      <td>Music</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Being George Clooney</td>
      <td>2016-02-06</td>
      <td>0</td>
      <td>0</td>
      <td>Documentary</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cold Souls</td>
      <td>2009-08-07</td>
      <td>0</td>
      <td>0</td>
      <td>Comedy</td>
    </tr>
  </tbody>
</table>
</div>




```python
movies_df.count()
```




    Movie           1049
    Release Date    1049
    Budget          1049
    Revenue         1049
    Genres          1049
    dtype: int64




```python
movies_df_clean2 = movies_df.drop_duplicates(keep= 'first')
```


```python
movies_df_clean2.count()
```




    Movie           562
    Release Date    562
    Budget          562
    Revenue         562
    Genres          562
    dtype: int64




```python
import csv
```


```python
movies_df_clean2.to_csv('MovieQuery2_Clean')
```


```python
movielist_2 = movies_df_clean2['Movie'].tolist()
print(movielist_2)
```

    ["Terrence Howard's Fright Club", 'I Am Heath Ledger', "I'm Still Here", 'Being George Clooney', 'Cold Souls', 'Jake Gyllenhaal Challenges the Winner of the Nobel Peace Prize', 'Judi Dench: My Passion for Trees', 'ハウルの動く城', 'Corpse Bride', 'Wallace & Gromit: The Curse of the Were-Rabbit', 'Good Night, and Good Luck.', 'Harry Potter and the Goblet of Fire', 'King Kong', 'Memoirs of a Geisha', 'Pride', 'Batman Begins', 'Brokeback Mountain', 'The Thinning: New World Order', 'Charlie and the Chocolate Factory', 'Mrs Henderson Presents', 'Walk the Line', 'Capote', 'Crash', 'Munich', "Darwin's Nightmare", 'Enron: The Smartest Guys in the Room', "La Marche de l'empereur", 'Murderball', 'Street Fight', 'The Death of Kevin Carter: Casualty of the Bang Bang Club', 'Cinderella Man', 'The Constant Gardener', "Don't Tell", 'Joyeux Noël', 'Paradise Now', 'Sophie Scholl – Die letzten Tage', 'Tsotsi', 'The Chronicles of Narnia: The Lion, the Witch and the Wardrobe', 'Star Wars: Episode III - Revenge of the Sith', 'Badgered', 'The Mysterious Geographic Explorations of Jasper Morello', '9', 'One Man Band', 'Cashback', 'Síðasti bærinn', 'Our Time Is Up', 'Six Shooter', 'War of the Worlds', 'A History of Violence', 'Match Point', 'The Squid and the Whale', 'Syriana', 'A Prairie Home Companion', 'Ryan Gosling - Hollywoods Halbgott', 'Will Smith: Live in Concert', 'Eddie Murphy Raw', 'When Harry Met Sally 2 with Billy Crystal and Helen Mirren', 'Cars', 'Happy Feet', 'Monster House', 'Dreamgirls', 'The Good Shepherd', 'El laberinto del fauno', "Pirates of the Caribbean: Dead Man's Chest", 'The Prestige', 'The Black Dahlia', 'Children of Men', 'The Illusionist', '滿城盡帶黃金甲', 'The Devil Wears Prada', 'Marie Antoinette', 'The Queen', 'Babel', 'The Departed', 'Letters from Iwo Jima', 'United 93', 'Deliver Us from Evil', 'An Inconvenient Truth', 'Iraq in Fragments', 'Jesus Camp', 'My Country No More', 'The Blood of Yingzhou District', 'Recycled Life', 'Two Hands', 'Blood Diamond', 'Efter brylluppet', 'Indigènes', 'Das Leben der Anderen', 'The Shape of Water', 'Apocalypto', 'Click', 'The Good German', 'Notes on a Scandal', 'Little Miss Sunshine', 'The Danish Poet', 'Lifted', 'The Little Matchgirl', 'Maestro', 'No Time for Nuts', 'Binta y la gran idea', 'Helmer & søn', 'Sultan: The Saviour', 'West Bank Story', 'Flags of Our Fathers', 'Poseidon', 'Superman Returns', 'Borat: Cultural Learnings of America for Make Benefit Glorious Nation of Kazakhstan', 'Little Children', 'Ennio Morricone: Arena concerto - la musica per il cinema', 'Richard Edlund VS His Sons', 'Johnny Depp - Idol, Rebell und Superstar', 'Tilda Swinton: The Love Factory', 'Persepolis', 'Ratatouille', "Surf's Up", 'American Gangster', 'Atonement', 'The Golden Compass', 'Sweeney Todd: The Demon Barber of Fleet Street', 'There Will Be Blood', 'The Assassination of Jesse James by the Coward Robert Ford', 'Le scaphandre et le papillon', 'No Country for Old Men', 'Across the Universe', 'Elizabeth: The Golden Age', 'La Môme', 'Juno', 'Michael Clayton', 'No End in Sight', 'Operation Homecoming: Writing the Wartime Experience', 'Sicko', 'Taxi to the Dark Side', 'War Dance', 'Freeheld', 'La corona partida', 'The Bourne Ultimatum', 'Into the Wild', 'בופור', 'The Counterfeiters', 'Katyń', 'Монгол', '12', 'Norbit', "Pirates of the Caribbean: At World's End", 'The Kite Runner', '3:10 to Yuma', 'I Met the Walrus', 'Madame Tutli-Putli', 'Peter Pan', 'Night at the Museum', 'Transformers', 'Away from Her', 'Lars and the Real Girl', 'The Savages', 'El Chapo & Sean Penn: Bungle in the Jungle', 'Michael Shannon Michael Shannon John', 'One Day', 'Bolt', 'Kung Fu Panda', 'Wall Street', 'Changeling', 'The Curious Case of Benjamin Button', 'The Dark Knight', 'The Duchess', 'Revolutionary Road', 'The Reader', 'Slumdog Millionaire', 'Australia', 'Milk', 'Frost/Nixon', 'The Betrayal (Nerakhoon)', 'Encounters at the End of the World', 'The Secret Garden', 'Man on Wire', 'Trouble the Water', 'The Conscience of Nhem En', 'Smile Pinki', 'Der Baader Meinhof Komplex', 'Front of the Class', 'Departures', 'Revanche', 'Vals Im Bashir', 'Hellboy II: The Golden Army', 'Defiance', 'つみきのいえ', 'Уборная история — любовная история', 'Oktapodi', 'Presto', 'This Way Up', 'The Only Living Boy in New York', 'Babe: Pig in the City', 'Spielzeugland', 'Iron Man', 'Wanted', 'Doubt', 'Frozen River', 'Happy-Go-Lucky', 'In Bruges', 'The Nutty Professor', 'Morgan Freeman Science Show - Esistono universi paralleli', 'Untitled Jeremy Renner/Bourne Sequel', 'Meeting Matt Damon', 'Premonition', 'Coraline', 'Fantastic Mr. Fox', 'The Princess and the Frog', 'The Secret of Kells', 'Up', 'Avatar', 'The Imaginarium of Doctor Parnassus', 'Nine', 'Sherlock Holmes', 'The Young Victoria', 'Harry Potter and the Half-Blood Prince', 'The Hurt Locker', 'Inglourious Basterds', 'Das weisse Band', 'Bright Star', 'Coco avant Chanel', 'Precious', 'Up in the Air', 'Burma VJ: Reporter i et lukket land', 'The Cove', 'Food, Inc.', 'The Most Dangerous Man in America: Daniel Ellsberg and the Pentagon Papers', 'Which Way Home', "China's Unnatural Disaster: The Tears of Sichuan Province", 'The Last Truck: Closing of a GM Plant', 'Music by Prudence', 'Królik po berlinsku', 'District 9', 'Ajami', 'La teta asustada', 'Anthem of a Teenage Prophet', 'El secreto de sus ojos', 'Il Divo', 'Star Trek', 'The Blind Side', 'An Education', 'A Serious Man', 'French Roast', "Granny O'Grimm's Sleeping Beauty", 'The Lady and the Reaper', 'Logorama', 'A Matter of Loaf and Death', 'The Girl Next Door', 'Instead of Abracadabra', 'കവി ഉദ്ദേശിച്ചത് ..?', 'Miracle Fish', 'The New Tenants', 'Transformers: Revenge of the Fallen', 'In the Loop', 'The Messenger', 'Lauren Bacall, ombre et lumière', "Roger Corman: Hollywood's Wild Angel", 'Comedy Central Roast of James Franco', 'Kathy Griffin is... Not Nicole Kidman', 'Untitled Jennifer Lawrence/Amy Schumer Project', 'Natalie Portman: Starting Young', 'How to Train Your Dragon', 'Toy Story 3', 'Alice in Wonderland', 'Harry Potter and the Deathly Hallows: Part 1', 'Inception', "The King's Speech", 'True Grit', 'Black Swan', 'The Social Network', 'Он - дракон', 'The Tempest', 'The Fighter', 'Exit Through the Gift Shop', 'Gasland', 'Inside Job', 'Restrepo', 'Waste Land', 'Strangers No More', '127 Hours', 'Biutiful', 'Κυνόδοντας', 'Hævnen', 'Incendies', 'Hors-la-loi', "Barney's Version", 'The Way Way Back', 'The Wolfman', 'The Kids Are All Right', "Winter's Bone", 'Groundhog Day', 'The Gruffalo', 'The Lost Thing', 'The Confession', 'The Crush', 'Eros, o Deus do Amor', 'Na Wewe', 'Wish 143', 'TRON: Legacy', 'Unstoppable', 'Salt', 'Hereafter', 'Iron Man 2', 'Another Year', 'Jean-Luc Cinema Godard', "Hearts of Darkness: A Filmmaker's Apocalypse", "Kenneth Branagh Theatre Company Live: The Winter's Tale", 'Nick Nolte: No Exit', 'Max Von Sydow: Dialogues with The Renter', 'Une vie de chat', 'Chico & Rita', 'Kung Fu Panda 2', 'Puss in Boots', 'Rango', 'The Artist', 'Harry Potter and the Deathly Hallows: Part 2', 'Hugo', 'Midnight in Paris', 'War Horse', 'The Girl with the Dragon Tattoo', 'The Tree of Life', 'Anonymous', 'Jane Eyre', 'W.E.', 'The Descendants', 'Hell and Back Again', 'If a Tree Falls: A Story of the Earth Liberation Front', 'Paradise Lost 3: Purgatory', 'Pina', 'Undefeated', 'The Barber of Birmingham: Foot Soldier of the Civil Rights Movement', 'God is the Bigger Elvis', 'Incident in New Baghdad', 'Saving Face', 'The Tsunami and the Cherry Blossom', 'Moneyball', 'Rundskop', 'הערת שוליים', 'In Darkness', 'Monsieur Lazhar', 'جدایی نادر از سیمین', 'Albert Nobbs', 'The Iron Lady', 'The Adventures of Tintin', 'Tinker Tailor Soldier Spy', 'Extremely Loud & Incredibly Close', 'The Help', 'Any Given Sunday', 'The Fantastic Flying Books of Mr Morris Lessmore', 'La Luna', 'Robinson Crusoe: The Wild Life', 'Pentecost', 'Raju Gadu', 'Love at the Shore', 'Time Freak', 'Tuba Atlantic', 'Drive', 'Transformers: Dark of the Moon', 'Real Steel', 'Rise of the Planet of the Apes', 'The Ides of March', 'Bridesmaids', 'Margin Call', "Mitch Albom's For One More Day", 'Alles wegen Robert De Niro', 'Brave', 'Frankenweenie', 'ParaNorman', 'The Pirates! In an Adventure with Scientists!', 'Wreck-It Ralph', 'Anna Karenina', 'Django Unchained', 'Life of Pi', 'Lincoln', 'Skyfall', 'Les Misérables', 'Mirror Mirror', 'Snow White and the Huntsman', 'Amour', 'Beasts of the Southern Wild', 'Silver Linings Playbook', 'Five Broken Cameras', 'The Gatekeepers', 'How to Survive a Plague', 'The Invisible War', 'Searching for Sugar Man', 'Born Innocent', 'Aprimi il cuore', 'The Shawshank Redemption', 'Argo', 'Zero Dark Thirty', 'Kon-Tiki', 'Dr. No', 'En kongelig affære', 'Rebelle', 'Hitchcock', 'The Hobbit: An Unexpected Journey', 'Adam and Dog', 'Fresh Guacamole', 'Head Over Heels', 'Maggie Simpson in The Longest Daycare', 'Paperman', 'Curfew', 'Hardcore Henry', 'The Avengers', 'Prometheus', 'Flight', 'Moonrise Kingdom', 'Jill Drew and D.A. Pennebaker', "George Stevens Jr. On 'Woman of the Year'", 'Joker', "Untitled Lupita Nyong'o/Rihanna Project", 'The Croods', 'Despicable Me 2', 'Ernest et Célestine', 'Frozen', '風立ちぬ', '一代宗師', 'Gravity', 'Inside Llewyn Davis', 'Nebraska', 'Prisoners', 'American Hustle', 'The Great Gatsby', 'The Invisible Woman', '12 Years a Slave', 'The Wolf of Wall Street', 'Jagal', 'Cutie and the Boxer', 'Dirty Wars', 'The Square', '20 Feet from Stardom', 'Cavedigger', 'Karama Has No Walls', 'Captain Phillips', 'Dallas Buyers Club', 'The Broken Circle Breakdown', 'The Great American Beauty Contest', 'Hunt for the Wilderpeople', "L'image manquante", "Omar m'a tuer", 'Jackass Presents: Bad Grandpa', 'The Lone Ranger', 'The Book Thief', 'Her', 'Philomena', 'Saving Mr. Banks', 'Feral', 'Get a Horse!', 'Mr Hublot', "Ava's Possessions", 'Room on the Broom', 'Avant que de tout perdre', 'Helium', 'The Voorman Problem', 'All Is Lost', 'The Hobbit: The Desolation of Smaug', 'Lone Survivor', 'Iron Man 3', 'Star Trek Into Darkness', 'Before Midnight', 'Blue Jasmine', 'Steve Martin Live', 'They All Laughed 25 Years Later: Director to Director - A Conversation with Peter Bogdanovich and Wes Anderson', 'Untitled Laura Dern/Judd Apatow Project', 'Big Hero 6', 'The Boxtrolls', 'How to Train Your Dragon 2', 'Song of the Sea', 'かぐや姫の物語', 'Birdman', 'The Grand Budapest Hotel', 'Ida', 'Mr. Turner', 'Unbroken', 'Inherent Vice', 'Into the Woods', 'Maleficent', 'Boyhood', 'Foxcatcher', 'The Imitation Game', 'Citizenfour', 'Finding Vivian Maier', 'Last Days in Vietnam', 'Salt of the Earth', 'Virunga', 'Crisis Hotline: Veterans Press 1', 'Joanna', 'Nasza klątwa', 'White Earth', 'American Sniper', 'Whiplash', 'Leviathan', 'Mandariinid', 'Timbuktu', 'Relatos salvajes', 'Guardians of the Galaxy', 'Interstellar', 'The Theory of Everything', 'Selma', 'The Bigger Picture', 'The Dam Keeper', 'Feast', 'Moulton og meg', 'A Single Life', 'Boogaloo and Graham', 'Parvaneh', 'The Phone Call', 'The Hobbit: The Battle of the Five Armies', 'Captain America: The Winter Soldier', 'Dawn of the Planet of the Apes', 'X-Men: Days of Future Past', 'Nightcrawler', 'Sing Your Song', 'Busy Bodies', 'Driven', 'Charlotte Rampling: The Look', 'Anomalisa', 'O Menino e o Mundo', 'Inside Out', 'Shaun the Sheep Movie', '思い出のマーニー', 'Carol', 'The Hateful Eight', 'Mad Max: Fury Road', 'The Revenant', 'Sicario', 'Cinderella', 'The Danish Girl', 'The Big Short', 'Room', 'Spotlight', 'Amy', 'Cartel Land', 'The Look of Silence', 'What Happened, Miss Simone?', "Winter on Fire: Ukraine's Fight for Freedom", 'Body Team 12', 'Chau, Beyond the Lines', 'A Girl in the River: The Price of Forgiveness', 'Last Day of Freedom', 'Star Wars: The Force Awakens', 'El Abrazo de la Serpiente', 'Mustang', 'Saul fia', 'Theeb\u200e\u200e', 'A Private War', 'Hundraåringen som klev ut genom fönstret och försvann', 'Bridge of Spies', 'The Bath Song & More Kids Songs: Super Simple Songs', 'Brooklyn', 'The Martian', 'Historia de un oso', 'Prologue', "Sanjay's Super Team", 'Мы не можем жить без космоса', 'World of Tomorrow', 'Ave Maria', 'Shok', 'Stutterer', 'Ex Machina', 'Straight Outta Compton', 'Bright Lights: Starring Carrie Fisher and Debbie Reynolds', 'He Got Game']
    


```python
print(len(movielist_2))
```

    562
    


```python

```
