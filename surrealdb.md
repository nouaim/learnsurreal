*Create first Table*
CREATE human:mark SET name="Mark", age=33, sex="Male";
CREATE human:daniel SET name="Daniel", age=29, sex="Male";

*To Select*
SELECT sex, name FROM human;
SELECT age, name FROM human WHERE age=29;


*Update*
UPDATE human SET skills +=["swimming", "football"];

*One-to-One Relationship*
UPDATE human:daniel SET best_friend = human:mark

*Fetch Data*
SELECT best_friend.name, best_friend.age FROM human:daniel;


*One-to-Many Relationship*
CREATE car:tesla
SET model='Model S', ev=true, price=99000;

CREATE car:renault
SET model='Clio 4', ev=false, price=30000;

UPDATE human:daniel SET cars=['car:tesla', 'car:renault'];

UPDATE car:tesla SET owner = human:daniel;
UPDATE car:renault SET owner = human:daniel;


*Query the data*
SELECT cars FROM human:daniel;
SELECT * FROM car WHERE owner==human:daniel;


*hasmanythrough relationship*
CREATE part:tire SET brand='IRIS', size=5;
CREATE part:gastank SET brand='NAFTAL', size=10;
CREATE part:battery SET brand='ELEC', size=9;


UPDATE car:tesla SET parts=['part:tire', 'part:battery'];
UPDATE car:renault SET parts=['part:tire', 'part:gastank'];


*Query*
SELECT parts FROM car:tesla;
SELECT cars.parts.brand FROM human:daniel;



*Graphs*
RELATE human:daniel -> drove -> car:tesla SET when = time::now(), destination= 'Market';
RELATE human:mark -> drove -> car:tesla SET when = time::now(), destination= 'Library';

*Query*
SELECT ->drove->car FROM human;

*change the arrows to the other direction to get the humans who drove the car*
SELECT <-drove<-human from car;


*Select everything from the drove table*
SELECT * FROM drove;



*Cli commands*

- To run in memeroy (database won't be saved)

```user@localhost % surreal start --log trace --user root --pass root memory```

- to save in file:

```user@localhost % surreal start --log trace --user root --pass root file:// ./Suerrealdb```


- To use it on command line:

```surreal sql --conn http://localhost:8000 -u root -p root```