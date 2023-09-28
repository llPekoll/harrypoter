<!-- HouseSelector.svelte -->
<script>
    let selectedHouse = "";
    let student = "";
    let studentImage = "";

    const houseGradients = {
        Gryffindor: "linear-gradient(135deg, #740001, #D3A625)",
        Hufflepuff: "linear-gradient(135deg, #FFDB58, #D3A625)",
        Ravenclaw: "linear-gradient(135deg, #222F5B, #42A0E4)",
        Slytherin: "linear-gradient(135deg, #1A472A, #5DAA68)",
    };

    const students = [
        {
            name: "Harry Potter",
            house: "Gryffindor",
            image: "https://media.tenor.com/84X3672KLCsAAAAC/harry-potter-harry-potter-characters.gif",
        },
        {
            name: "Hermione Granger",
            house: "Gryffindor",
            image: "https://media.tenor.com/qYySZ9y7e2YAAAAC/hermione-granger-wand.gif",
        },
        {
            name: "Draco Malfoy",
            house: "Slytherin",
            image: "https://media.tenor.com/o2WNfXdy6bsAAAAC/draco-malfoy.gif",
        },
        {
            name: "Luna Lovegood",
            house: "Ravenclaw",
            image: "https://media.tenor.com/gK7hHQiFXkcAAAAC/spookymrg.gif",
        },
        {
            name: "Cedric Diggory",
            house: "Hufflepuff",
            image: "https://media.tenor.com/Igq9J8-cWqwAAAAC/cedric-diggory-hufflepuff.gif",
        },
        // Add more students with their names, houses, and image URLs
    ];

    // Function to change the background gradient, show a random student from the selected house, and update the student image
    const chooseStudent = (house) => {
        if (house) {
            // Filter students based on the selected house
            const houseStudents = students.filter(
                (student) => student.house === house
            );

            // Select a random student from the filtered list
            const randomStudent =
                houseStudents[Math.floor(Math.random() * houseStudents.length)];

            if (randomStudent) {
                student = randomStudent.name;
                studentImage = randomStudent.image;
                selectedHouse = house;

                // Set the background gradient based on the selected house
                document.body.style.backgroundImage =
                    houseGradients[selectedHouse];

                // Reset text color to default (white) for better contrast
                document.body.style.color = "white";
            } else {
                student = "";
                studentImage = "";

                // Reset the background gradient
                document.body.style.backgroundImage = "";
            }
        }
    };
</script>

<div>
    <!-- Buttons to choose Harry Potter houses -->
    <button
        on:click={() => {
            chooseStudent("Gryffindor");
        }}>Gryffindor</button
    >
    <button
        on:click={() => {
            chooseStudent("Hufflepuff");
        }}>Hufflepuff</button
    >
    <button
        on:click={() => {
            chooseStudent("Ravenclaw");
        }}>Ravenclaw</button
    >
    <button
        on:click={() => {
            chooseStudent("Slytherin");
        }}>Slytherin</button
    >
</div>

<p>
    {selectedHouse
        ? `You chose a student from ${selectedHouse}!`
        : "Select a house to choose a student."}
</p>

{#if student}
    <p>A student appears: {student}</p>
    {#if studentImage}
        <img src={studentImage} alt={student} />
    {/if}
{/if}

<style>
    /* Add your CSS styles here (optional) */
</style>
