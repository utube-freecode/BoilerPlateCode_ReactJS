# BoilerPlateCode_ReactJS

Boiler Plate Code - React JS


1. Terminal -> npx create-react-app my-react-app
2. cd my-react-app
3. Terminal -> npm start
4. /myReactApp/src/App.js file -> 
    1. function App() {
    2. return (
    3. <div className="App">
    4. <h1>Hello World!</h1>
    5. </div>
    6. );
    7. }
    8. export default App;
5. If there is error of Cannot find module 'ajv/dist/compile/codegen' Require stack then follow this steps -> 
    1. Terminal -> rm -rf node_modules
    2. Terminal -> rm package-lock.json
    3. Terminal -> npm install
    4. Terminal -> npm cache clean --force
    5. Terminal -> npm install ajv@latest ajv-keywords@latest
    6. Terminal -> npm install react-scripts@latest
    7. Terminal -> npm install ajv
6. Terminal -> npm i axios bootstrap react-router-dom
7. Index.js file -> import { BrowserRouter, Route, Routes } from 'react-router-dom';
    1. <BrowserRouter>
    2. <Routes>
    3. <Route index element={<App />}/>
    4. <Route path='dashboard' element={<Dashboard />}/>
    5. </Routes>
    6. </BrowserRouter>
8. App.js file -> import { useState } from 'react';
9. App.js file -> import { useNavigate } from 'react-router-dom';
    1. function App() {
    2. const [uname,setUname] = useState();
    3. const [pass,setPass] = useState();
    4. const navigate = useNavigate();
    5. const handleLogin = () => {
    6. if(uname === "admin" && pass === "admin"){
    7. alert("Login Success");
    8. navigate("/dashboard");
    9. }
    10. else{
    11. alert("Invalid Input");
    12. }
    13. }
    14. return (
    15. <div className='centr'><input className='inpt' type='text' name='username' placeholder='Enter Usernmae' onChange={uname => setUname(uname.target.value)}/>
    16. <input className='inpt2' type=‘password name='pass' placeholder='Enter Password' onChange={pass => setPass(pass.target.value)}/>
    17. <p> Username - {uname} </p>
    18. <p> pass - {pass} </p>
    19. <button className='buttons' onClick={handleLogin} >Login</button>    
    20. </div>
    21. );
    22. }
    23. export default App;
10. App.css file -> 
    1. .centr {
    2. display: flex;
    3. align-items: center;
    4. flex-direction: column;
    5. }
    6. .inpt {
    7. margin-top: 5%;
    8. width: 40%;
    9. height: 35px;
    10. font-size: 15px;
    11. padding-left: 1%;
    12. }
    13. .inpt2 {
    14. margin-top: 2%;
    15. width: 40%;
    16. height: 35px;
    17. font-size: 15px;
    18. padding-left: 1%;
    19. }
    20. .btn {
    21. margin-top: 2%;
    22. height: 25px;
    23. width: 10%;
    24. font-size: 15px;
    25. }
11. Dashboard.js file -> import axios from 'axios';
    1. function Dashboard() {
    2. const [data, setData] = useState();
    3. const [users, setUsers] = useState();
    4. const [userId, setUserId] = useState();
    5. const [id, setId] = useState();
    6. const [title, setTitle] = useState();
    7. useEffect(() => {
    8. fetch("https://reqres.in/api/users?page=2")
    9. .then(res => {
    10. return res.json()
    11. })
    12. .then(jsn => {
    13. console.log(jsn)
    14. setData(jsn.data)
    15. })
    16. .catch(error => {
    17. console.log(error)
    18. })
    19. }, [])
    20. useEffect(() => {
    21. axios.get("https://reqres.in/api/users")
    22. .then(res => {
    23. return res.data
    24. })
    25. .then(jsn => {
    26. console.log(jsn);
    27. setUsers(jsn.data);
    28. })
    29. .catch(error => {
    30. console.log(error);
    31. })
    32. }, [])
    33. const handlePostApi = () => {
    34. axios.post("https://jsonplaceholder.typicode.com/posts", {
    35. userId : userId,
    36. id : id,
    37. title : title
    38. })
    39. .then(res => {
    40. return res.data
    41. })
    42. .then(data => {
    43. console.log(data)
    44. })
    45. .catch(error => {
    46. console.log(error)
    47. })
    48. }
    49. return (
    50. <div className='App'>
    51. <h2>Dashboard</h2>
    52. {data && data.map(data => {
    53. return(<div key={data.id}>
    54. <h3>{data.id}</h3>
    55. <h4>{data.email}</h4>
    56. <h5>{data.first_name}</h5>
    57. <h6>{data.last_name}</h6>
    58. </div>
    59. )
    60. })}
    61. {users && users.map(data => {
    62. return(
    63. <div key={data.id}>
    64. <h3>{data.id}</h3>
    65. <h4>{data.email}</h4>
    66. <h5>{data.first_name}</h5>
    67. <h6>{data.last_name}</h6>
    68. </div>
    69. )
    70. })}
    71. <input type='text' name='userId' placeholder='Enter user id' onChange={val => setUserId(val.target.value)} />
    72. <input type='text' name='id' placeholder='Enter id' onChange={val => setId(val.target.value)} />
    73. <input type='text' name='title' placeholder='Enter title' onChange={val => setTitle(val.target.value)} />
    74. <button type='submit' className='btn' onClick={handlePostApi}>POST API</button>
    75. </div>
    76. );
    77. }
    78. export default Dashboard;
12. 
