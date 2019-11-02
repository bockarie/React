# Homework Submission

All homework should be within this directory, and this directory only. Please place your homework in a directory anywhere at `/homework-submission/*`, eg: `/homework-submission/my-project/package.json`.

Homework is then submitted via PR in the normal way.

Homework will not be reviewed unless:

1. Your PR _only_ modifies the `homework-submission` directory
2. Your PR passes linting


Homework3


import React from 'react'
import { BrowserRouter as Router, Switch ,} from "react-router-dom";

import Menu from "./Components/Menu";
import DetailComponent from "./Components/DetailComponent";
import CreateComponent from "./Components/CreateComponent";
//import "antd/dist/antd.css";
import './App.css';
import ListComponent from './Components/ListComponent';
import DataFetching from './Components/DataFetching';
function App() {
  return (
    <div className="App">
      <Router>
        <Menu />
        <Switch>
          <Router path="/create" exact>
            <CreateComponent/>
          </Router>

         <Router path="/:id">
           <DetailComponent/>
         </Router>
         <Router path="/" exact>
           <ListComponent/>
           <DataFetching/>
         </Router>
        </Switch>
      </Router>
    </div>
  ); 
}

export default App;




const CreateComponent = () => {

    return <div>create</div>
        
    
};
export default CreateComponent;




import React from "react";
import { useParams} from "react-router";

const DetailComponent = (props) => {
     const { id} = useParams();

    return <div>detail: {id}</div>;

    
};
export default DetailComponent;



import React, { useState } from "react";
import { Link} from "react-router-dom";
const Menu = ({}) => {
  return (
  <div>
    <Link to="/">Home</Link>
    <Link to="/create">Create new</Link>
    </div>
  );
};

export default Menu;


import React from "react";

const ListComponent = () => {
    return <div>list</div>
};
export default ListComponent;



import React,{useState, useEffect} from 'react';
import axios from 'axios';

function DataFetching() {
    const [posts,setPosts] = useState([])

    useEffect(() => {
        axios.get('https://jsonplaceholder.typicode.com/post')
        .then( res => {
            console.log(res)
            setPosts(res.data)
        })
        .catch(err => {
            console.log(err)
        })
        

    }, [])
    return(
        <div>
            <ul>
                {posts.map(post => (<li key={post.id}>{post.title}</li>))}
            </ul>

        </div>
    )
}
export default DataFetching;
