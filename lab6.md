app
```jsx
import { useState,useEffect,useCallback } from "react";
import DOMPurify from "dompurify";
import "./index.css";
const Form = () => {
    const [formData, setFormData] = useState({
        name: "",
        email: "",
        password: "",
    });
    const [errors, setErrors] = useState({});
    const [submittedData, setSubmittedData] = useState(null);
    const [showPassword, setShowPassword] = useState(false);
    const [isFormValid, setIsFormValid] = useState(false);
    const sanitizeInput = (value)=>DOMPurify.sanitize(value);
    const handleChange=(e)=>{
        const{name,value}=e.target;
        setFormData((prev)=>({
            ...prev,
            [name]:sanitizeInput(value.trim()),
        }));
    };
    const validateForm=useCallback(()=>{
        let valid=true;
        const newErrors={};
        if(!formData.name){
            newErrors.name="Name is required";
            valid=false;
        }
        const emailPattern=
            /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
        if(!formData.email){
            newErrors.email="Email is required";
            valid=false;
        }
        else if(!emailPattern.test(formData.email)){
            newErrors.email="Enter valid email";
            valid=false;
        }
        const passwordPattern=
            /^(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&]).{6,}$/;
        if(!formData.password){
            newErrors.password="Password is required";
            valid=false;
        }
        else if(!passwordPattern.test(formData.password)){
            newErrors.password=
                "Min 6 chars, 1 uppercase, 1 number, 1 special char";
            valid=false;
        }
        setErrors(newErrors);
        setIsFormValid(valid);
    },[formData]);
    useEffect(()=>{
        validateForm();
    },[formData,validateForm]);
    const handleSubmit=(e)=>{
        e.preventDefault();
        if(isFormValid){
            setSubmittedData(formData);
            setFormData({
                name: "",
                email: "",
                password: "",
            });
        }
    };
    return (
        <div className="form-container">
            <h2>Registration Form</h2>
            <form onSubmit={handleSubmit}>
                <div className="form-group">
                    <label>Name</label>
                    <input 
                        type="text" 
                        name="name" 
                        value={formData.name} 
                        onChange={handleChange}
                        className={errors.name ? "error-border" : ""}
                        placeholder="Enter name" 
                    />
                    {errors.name&&
                        <div className="error-message">
                            {errors.name}
                        </div>
                    }
                </div>
                <div className="form-group">
                    <label>Email</label>
                    <input
                        type="email"
                        name="email"
                        value={formData.email}
                        onChange={handleChange}
                        className={errors.email ? "error-border" : ""}
                        placeholder="Enter email"
                    />
                    {errors.email&&
                        <div className="error-message">
                            {errors.email}
                        </div>
                    }
                </div>
                <div className="form-group">
                    <label>Password</label>
                    <input 
                        type={showPassword ? "text" : "password"} 
                        name="password" 
                        value={formData.password} 
                        onChange={handleChange} 
                        className={errors.password ? "error-border" : ""}
                        placeholder="Enter password"
                    />
                    {errors.password&&
                        <div className="error-message">
                            {errors.password}
                        </div>
                    }
                </div>
                <div className="form-group">
                    <label>
                        <input 
                            type="checkbox"
                            checked={showPassword}
                            onChange={()=>
                                setShowPassword(!showPassword)
                            }
                        />
                        Show Password
                    </label>
                </div>
                <button
                    type="submit"
                    disabled={!isFormValid}
                >
                    Submit
                </button>
            </form>
        {submittedData&&(
            <div className="result">
                <h3>Sumitted Data</h3>
                <p>Name: {submittedData.name}</p>
                <p>Email: {submittedData.email}</p>
                <p>Password: {submittedData.password}</p>
            </div>
        )}
    </div>
    );
};
export default Form;
```

index
```css
body {
  font-family: Arial, Helvetica, sans-serif;
  background-color: #f4f6f9;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}
.form-container {
  background: #fff;
  padding: 25px 30px;
  border-radius: 8px;
  width: 350px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}
.form-container h2 {
  text-align: center;
  margin-bottom: 20px;
}
.form-group {
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
}
label {
  margin-bottom: 5px;
  font-weight: 500;
}
input[type="text"],
input[type="email"],
input[type="password"] {
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  font-size: 14px;
  transition: border 0.3s;
}
input:focus {
  outline: none;
  border: 1px solid #4caf50;
}
.error-border {
  border: 1px solid red !important;
}
.error-message {
  color: red;
  font-size: 12px;
  margin-top: 4px;
}
button {
  width: 100%;
  padding: 10px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 15px;
  transition: background-color 0.3s;
}
button:hover {
  background-color: #45a049;
}
button:disabled {
  background-color: #a5d6a7;
  cursor: not-allowed;
}
.result {
  margin-top: 20px;
  padding: 15px;
  background-color: #f0f8f5;
  border-radius: 6px;
  font-size: 14px;
}
```
