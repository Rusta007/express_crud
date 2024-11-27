# express_crud


let students = [
    {
        id: 1,
        name: "John Doe", 
        age: 20,
        course: "Computer Science"
    },
    {
        id: 2,
        name: "Jane Doe", 
        age: 21,
        course: "Computer Science"
    }
]

app.get('/', (req, res) => {
    console.log("from server");
    res.sendStatus(404)
    res.send("Hello World!!")
})

app.get('/students', (req, res) => {
    res.send(students)
})

app.post('/students', (req, res) => {
    // let newStudents = [{
    //     id: 3,
    //     name: "John Doe", 
    //     age: 20,
    //     course: "Computer Science"
    // }]

    // students = [...students, ...newStudents]
    // res.send(students)
    // res.sendStatus(201)
    // res.send("Student added")
    // res.send(newStudents)

    const {name, age, course} = req.body


    console.log(req.body)
    const newStudent = {
        id: students.length + 1,
        name: name, 
        age: age,
        course: course
    }
    students = [...students, newStudent]
    res.send(students)
    res.sendStatus(201)
    res.send("Student added")
    res.send(newStudent)


})

app.put('/students/:id', (req, res) => {
    const {id} = req.params
    console.log(req.params)

    const {name, age, course} = req.body
    
    const student = students.find(student => student.id == parseInt(id))
    
    student.name = name
    student.age = age
    student.course = course
   
    res.send(students)
})

app.delete('/students/:id', (req, res) => {
    const {id} = req.params
    students = students.filter(student => student.id != id)
    res.send(students)
})
