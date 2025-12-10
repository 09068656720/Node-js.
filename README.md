# Node-js.

// index.js
const mongoose = require('mongoose');
const connectDB = require('./config/db');
const Student = require('./models/Student');

const MONGO_URI = 'mongodb:                             

async function run() {
  try {
    await connectDB(MONGO_URI);
    console.log('//localhost:27017/school_db';

async function run() {
  try {
    await connectDB(MONGO_URI);
    console.log('Database connected successfully. Starting operations...');

    console.log('\n--- 4. Inserting New Student ---');
    const newStudent = new Student({
      name: 'Alice Johnson',
      department: 'Computer Science',
      level: 300
    });
    const savedStudent = await newStudent.save();
    console.log(` Successfully inserted student: ${savedStudent.name} (ID: ${savedStudent._id})`);

    console.log('\n--- 5. Querying All Students ---');
    const allStudents = await Student.find({});
    if (allStudents.length === 0) {
      console.log('No students found in the database.');
    } else {
      console.log(`Found ${allStudents.length} student(s):`);
      allStudents.forEach((student, index) => {
        console.log(` ${index + 1}. Name: ${student.name}, Dept: ${student.department}, Level: ${student.level}`);
      });
    }
  } catch (error) {
    console.error('\n An error occurred during database operations:', error.message);
    process.exit(1);
  } finally {
    if (mongoose.connection.readyState === 1) {
      await mongoose.disconnect();
      console.log('\nDatabase connection closed.');
