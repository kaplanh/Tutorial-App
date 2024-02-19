# Tutorial App (CRUD Operations with Axios)

[:point_right: Click here to see on browser]()

![tasktraker]


---

| **What's used in this app ?**                         | **How use third party libraries**          | **Author**                                                     |
| ----------------------------------------------------- | ------------------------------------------ | -------------------------------------------------------------- |
| [useEfect() Hook componentDidUpdate()](https://react.dev/learn#using-hooks)|                                            | [Take a look at my portfolio](https://kaplanh.github.io/Portfolio_with_CssFlex/) |
| [useState() Hook](https://react.dev/learn#using-hooks)|                                            | [Visit me on Linkedin](https://www.linkedin.com/in/kaplan-h/)                    |
| [CRUD OPERATIONS with axios API](https://www.npmjs.com/package/axios#axios-api) | npm i/yarn add axios                        |                    |
| [react-events](https://react.dev/learn#responding-to-events)|                                      |                    |
| [Bootstrap](https://getbootstrap.com/docs/5.3/getting-started/introduction/) | npm i / yarn add bootstrap & index.html'e <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-geWF76RCwLtnZ8qwWowPQNguL3RmwHVBC9FhGdlKrxdiJJigb/j/68SIy3Te4Bkz"
      crossorigin="anonymous"
    ></script>                   |                    |
| [React-icons](https://react-icons.github.io/react-icons/)| npm i / yarn add react-icons               |                 |
| [props-drilling](https://react.dev/learn#sharing-data-between-components)|                            |                 |
| [Semantic-Commits](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716) |             |                 |
| Deploy with [Netlify](https://app.netlify.com/teams/kaplanh/sites) |                                 |                 |

---

## How To Run This Project 🚀

<br/>

### 💻 Install React 👇

```bash
yarn create react-app .  or npx create-react-app .
```

### 💻 Install Sass 👇

```bash
yarn add sass  or npm i sass
```

## 🔴 Delete these files and delete the imports👇

    - App.test.js
    - reportWebVitals.js
    - setupTests.js
    - favicon.ico
    - logo192.png
    - logo512.png
    - manifest.json
    - robots.txt

### 💻 Start the project 👇

```bash
yarn start or npm start
```

OR

-   <strong>Clone the Repo</strong>

    ```sh
    git clone
    ```

-   <strong>Install NPM packages</strong>

    ```sh
    npm install or yarn
    ```

-   <strong>Run the project</strong>

    ```sh
    npm start or yarn start
    ```

-   <strong>Open the project on your browser</strong>

    ```sh
    http://localhost:3000/
    ```

-   ### <strong>Enjoy! 🎉</strong>

---

## Project Skeleton

```
 Tutorial App(folder)
|
|----public (folder)
│     └── index.html
|----src (folder)
|    |--- components (folder)
│    │       ├── AddTutorial.jsx
│    │       ├── EditTutorial.jsx
│    │       ├── TutorialList.jsx
│    │
│    │
│    |--- pages (folder)
|    |      ├── Home.jsx
|    |
│    ├--- App.js
│    |--- index.js
│
│
|-- .gitignore
|── package-lock.json
├── package.json
|── README.md
|── yarn.lock


```

---
### At the end of the project, the following topics are to be covered;

- CRUD(READ-GET with axios)useEffect()  (componentDidUpdate() ) & useState() & onChange, onSubmit Events

- 
 ```jsx
    import { useEffect, useState } from "react";
    import AddTutorial from "../components/AddTutorial";
    import TutorialList from "../components/TutorialList";
    import axios from "axios";
    
    const Home = () => {
        const [tutorials, setTutorials] = useState([]);
    
        const getTutorials = async () => {
            const BASE_URL =
                "https://tutorial-api.fullstack.clarusway.com/tutorials/";
            try {
                // const res = await axios(BASE_URL)
                // setTutorials(res.data)
                const { data } = await axios(BASE_URL);
                setTutorials(data);
            } catch (error) {
                console.log(error);
            }
        };
    
        console.log(tutorials);
    
        //? Mount asamasinda api'ye istek atiyoruz
        useEffect(() => {
            getTutorials();
        }, []);
    
        return (
            <>
                <AddTutorial getTutorials={getTutorials} />
                <TutorialList tutorials={tutorials} getTutorials={getTutorials} />
            </>
        );
    };
    
    export default Home;
     
 ```
- CRUD(CREATE-POST with axios)

    ```jsx
      import { useState } from "react";
      import axios from "axios";
    
     const AddTutorial = ({ getTutorials }) => {
        const [title, setTitle] = useState("");
        const [description, setDescription] = useState("");

    const handleSubmit = (e) => {
        e.preventDefault();
        const newTutor = { title: title, description: description };
        console.log(newTutor);
        postTutorial(newTutor);

        setTitle("");
        setDescription("");
    };

    const postTutorial = async (newTutor) => {
        const BASE_URL =
            "https://tutorial-api.fullstack.clarusway.com/tutorials/";
        try {
            const res = await axios.post(BASE_URL, newTutor);
            console.log(res);
        } catch (error) {
            console.log(error);
        }

        //? Tum tutorial'lari iste ve state'i guncelle
        getTutorials();
    };

    return (
        <div className="container text-center mt-4">
            <h1 className="display-6 text-danger">Add Your Tutorial</h1>
            <form onSubmit={handleSubmit}>
                <div className="mb-3">
                    <label htmlFor="title" className="form-label">
                        Title
                    </label>
                    <input
                        type="text"
                        className="form-control"
                        id="title"
                        placeholder="Enter your title"
                        value={title}
                        onChange={(e) => setTitle(e.target.value)}
                        required
                    />
                </div>
                <div className="mb-3">
                    <label htmlFor="desc" className="form-label">
                        Description
                    </label>
                    <input
                        type="text"
                        className="form-control"
                        id="desc"
                        placeholder="Enter your Description"
                        value={description}
                        onChange={(e) => setDescription(e.target.value)}
                        required
                    />
                </div>
                <button type="submit" className="btn btn-danger mb-4">
                    Submit
                </button>
            </form>
        </div>
    );
    };
    
    export default AddTutorial;

       
    ```

- CRUD(UPDATE-PUT  with axios)useEffect()  (componentDidUpdate() ) & useState() & onChange, onSubmit Events

 ```jsx
        import axios from "axios";
        import { useEffect, useState } from "react";
        
        const EditTutorial = ({ editItem, getTutorials }) => {
            console.log(editItem);
        
            const { id, description: oldDescription, title: oldTitle } = editItem;
            console.log("old", oldTitle);
            console.log("old", oldDescription);
            //? https://react.dev/reference/react/useState#usestate
            //! State degiskeninin degeri, 1.render ile initialState
            //! parametresinin ilk degerini alir. Dolayisiyle bu durumda
            //! prop'tan gelen ilk deger state'e aktarilir.
            //! Sonradan degisen props degerleri useState'e aktarilmaz.
            //! Eger props'tan gelen degerleri her degisimde useState'e
            //! aktarmak istersek useEffect hook'unu componentDidUpdate
            //! gibi kullanabiriz.
            const [title, setTitle] = useState(oldTitle);
            const [description, setDescription] = useState(oldDescription);
        
            //? componentDidUpdate
            useEffect(() => {
                setTitle(oldTitle);
                setDescription(oldDescription);
                //? oldTitle veya oldDescriptiion her degistiginde local title ve description state'lerimizi guncelliyoruz.
            }, [oldTitle, oldDescription]);
        
            console.log(title); //ilk render da undefined
            console.log(description);
        
            const editTutor = async (tutor) => {
                const BASE_URL =
                    "https://tutorial-api.fullstack.clarusway.com/tutorials";
        
                try {
                    await axios.put(`${BASE_URL}/${id}/`, tutor);
                } catch (error) {
                    console.log(error);
                }
                getTutorials();
            };
            const handleSubmit = (e) => {
              e.preventDefault();
             
              editTutor({ title, description });
              // !yada objeyi degiskene atayip parametre olarak gönderebiliriz
              //  const tutor = {
              //      title,
              //      description,
              //  };
              //  editTutor(tutor);
            };
        
            return (
                <div
                    className="modal fade"
                    id="open-modal"
                    tabIndex={-1}
                    aria-labelledby="exampleModalLabel"
                    aria-hidden="true"
                >
                    <div className="modal-dialog">
                        <div className="modal-content">
                            <div className="modal-header">
                                <h1
                                    className="modal-title text-danger fs-5"
                                    id="exampleModalLabel"
                                >
                                    Edit Tutorial
                                </h1>
                                <button
                                    type="button"
                                    className="btn-close"
                                    data-bs-dismiss="modal"
                                    aria-label="Close"
                                    onClick={() => {
                                        setDescription("");
                                        setTitle("");
                                    }}
                                />
                            </div>
                            <div className="modal-body">
                                <form onSubmit={handleSubmit}>
                                    <div className="mb-3">
                                        <label htmlFor="title" className="form-label">
                                            Title
                                        </label>
                                        <input
                                            type="text"
                                            className="form-control"
                                            id="title"
                                            placeholder="Enter your title"
                                            value={title || ""}
                                            onChange={(e) => setTitle(e.target.value)}
                                            required
                                        />
                                    </div>
                                    <div className="mb-3">
                                        <label htmlFor="desc" className="form-label">
                                            Description
                                        </label>
                                        <input
                                            type="text"
                                            className="form-control"
                                            id="desc"
                                            placeholder="Enter your Description"
                                            value={description || ""}
                                            onChange={(e) =>
                                                setDescription(e.target.value)
                                            }
                                            required
                                        />
                                    </div>
        
                                    <div className="text-end">
                                        <button
                                            type="submit"
                                            className="btn btn-danger"
                                            data-bs-dismiss="modal"
                                        >
                                            Submit
                                        </button>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                </div>
            );
        };
        
        export default EditTutorial;

    
 ```



-  CRUD(DELETE-DELETE with Axios)

    ```jsx
            import { FaEdit } from "react-icons/fa";
            import { AiFillDelete } from "react-icons/ai";
            import axios from "axios";
            import EditTutorial from "./EditTutorial";
            import { useState } from "react";
            
            const TutorialList = ({ tutorials, getTutorials }) => {
                const [editItem, setEditItem] = useState("");
        
            console.log(editItem);
            // const tutorials = [
            //   {
            //     id: 1,
            //     title: "JS",
            //     description: "JS is a programming language",
            //   },
            //   {
            //     id: 2,
            //     title: "React",
            //     description: "JS library for UI design",
            //   },
            //   {
            //     id: 3,
            //     title: "VUE",
            //     description: "JS library for UI design",
            //   },
            // ]
            const BASE_URL = "https://tutorial-api.fullstack.clarusway.com/tutorials";
        
            const handleDelete = async (id) => {
                try {
                    await axios.delete(`${BASE_URL}/${id}/`);
                } catch (error) {
                    console.log(error);
                }
                getTutorials();
            };
        
            // const editTutor = async (tutor) => {
            //   try {
            //     await axios.put(`${BASE_URL}/${tutor.id}/`, tutor)
            //   } catch (error) {
            //     console.log(error)
            //   }
            //   getTutorials()
            // }
        
            return (
                <div className="container mt-4">
                    <table className="table table-striped">
                        <thead>
                            <tr>
                                <th scope="col">#id</th>
                                <th scope="col">Title</th>
                                <th scope="col">Description</th>
                                <th scope="col" className="text-center">
                                    Edit
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            {tutorials?.map((item) => {
                                const { id, title, description } = item;
                                return (
                                    <tr key={id}>
                                        <th>{id}</th>
                                        <td>{title}</td>
                                        <td>{description}</td>
                                        <td className="text-center text-nowrap">
                                            <FaEdit
                                                size={20}
                                                type="button"
                                                className="me-2 text-warning"
                                                data-bs-toggle="modal"
                                                data-bs-target="#open-modal"
                                                // onClick={() =>
                                                //   editTutor({
                                                //     id: 1934,
                                                //     title: "REACT",
                                                //     description: "JS Library",
                                                //   })
                                                // }
        
                                                onClick={() => setEditItem(item)}
                                            />
                                            <AiFillDelete
                                                size={22}
                                                type="button"
                                                className="text-danger "
                                                onClick={() => handleDelete(id)}
                                            />
                                        </td>
                                    </tr>
                                );
                            })}
                        </tbody>
                    </table>
        
                    <EditTutorial editItem={editItem} getTutorials={getTutorials} />
                </div>
            );
        };
        
        export default TutorialList;

    ```

-   Semantic Commit Messages
    See how a minor change to your commit message style can make you a better programmer.

    Format: <type>(<scope>): <subject>

    <scope> is optional

    -   Example

    ```
                feat: add hat wobble
        ^--^  ^------------^
        |     |
        |     +-> Summary in present tense.
        |
        +-------> Type: chore, docs, feat, fix, refactor, style, or test.
    ```

- More Examples:
    -   `feat`: (new feature for the user, not a new feature for build script)
    -   `fix`: (bug fix for the user, not a fix to a build script)
    -   `docs`: (changes to the documentation)
    -   `style`: (formatting, missing semi colons, etc; no production code change)
    -   `refactor`: (refactoring production code, eg. renaming a variable)
    -   `test`: (adding missing tests, refactoring tests; no production code change)
    -   `chore`: (updating grunt tasks etc; no production code change)

---

## Feedback and Collaboration

I value your feedback and suggestions. If you have any comments, questions, or ideas for improvement regarding this project or any of my other projects, please don't hesitate to reach out.
I'm always open to collaboration and welcome the opportunity to work on exciting projects together.
Thank you for visiting my project. I hope you have a wonderful experience exploring it, and I look forward to connecting with you soon!

<p align="center"> ⌛<strong> Happy Coding </strong> ✍ </p>
