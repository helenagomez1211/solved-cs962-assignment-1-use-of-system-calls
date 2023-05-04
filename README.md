Download Link: https://assignmentchef.com/product/solved-cs962-assignment-1-use-of-system-calls
<br>
This programming assignment makes you acquainted with the working principle of system calls. You need to establish a communication channel between two processes to achieve different functionalities as described in each task. You can download/clone the code base and all other relevant files for PA1

from the following link <a href="https://github.com/skmtr1/emasters-os-2022-PA1.git">https://github.com/skmtr1/emasters-os-2022-PA1.git</a><a href="https://github.com/skmtr1/emasters-os-2022-PA1.git">.</a> Template code for tasks are placed under the root folder in respective folders—Task-1, Task-2 and Task-3. Please go through the README file to understand the code base structure and build process of the assignment.

<h2>Task 1: Lets Do Some Calculation !!!! Client-Server Calculator</h2>

In this task, you need to implement a client-server based calculator. The client can submit any number of queries (i.e. mathematical expressions) to the server. The server will evaluate client’s queries one by one and send back the answer as a response.

In this task, the client-server pair is created by fork where child process acts as the server and the parent as client. The server will respond to all queries submitted by the client until it receives a specific terminating word (mentioned below) as a query from the client. After receiving the specific terminating word, the server will close the communication channel and exits. You need to use pipe to establish a communication channel between client and server.

Figure 1 shows the workflow of this client-server based calculator using pipes. The client (parent) should read expression (or may be terminating word) from standard input device, and will display

Figure 1: Workflow of client-server based calculator.

result received from the server on standard output device as shown in the figure.

<strong>Requirement specifications for this task are as follows:</strong>

<ol>

 <li>Input expression is always space separated, i.e. blank space between operand and operator.</li>

 <li>Input expression always starts with an operand.</li>

 <li>Input expression can have at most 20 operands (i.e., it can have at most 19 operators).</li>

 <li>Operands in input expression may be an integer or float/double number.</li>

 <li>Input expression can contain any combination of these five operators viz. (i) Addition (<strong>+</strong>), (ii) Subtraction (<strong>–</strong>), (iii) Multiplication (<strong>*</strong>), (iv) Division (<strong>/</strong>), and modulo (<strong>%</strong>).</li>

 <li>When server performs calculation, it needs to follow <strong>BODMAS </strong>rule where division, multiplication and modulo operators are at same precedence (say precedence-1) and addition and subtraction are at precedence-2. According to BODMAS, server should first perform precedence-1 operations followed by precedence-2 operations. Among same precedence operations, server should perform operation from left to right.</li>

 <li>When client receives <strong>END </strong>word from STDIN, it should send a termination signal to the server to terminate it properly.</li>

 <li>On receiving the result of mathematical expressions from the server, client should print <strong>“RESULT: ” </strong>followed by result. As an example, if client receive <strong>5 </strong>from the server, then it should display <strong>“RESULT: 5” </strong>on STDOUT.</li>

</ol>

<strong>Example of Input &amp; Output:</strong>

[INPUT] 1 + 5 * 2 – 1 + 10

[OUTPUT] RESULT: 20

[INPUT] 5 + 1 – 2 * 5 + 10

[OUTPUT] RESULT: 6

[INPUT] END

<h3>Implementation</h3>

<ul>

 <li>Inside <strong>Task-1 </strong>folder, you will find four C files namely—(i) <strong>c</strong>, (ii) <strong>task1_calculate.c</strong>, (iii) <strong>task1_client.c</strong>, and (iv) <strong>task1_server.c</strong>.</li>

 <li>You need to establish the communication channel and invoke the client and server function at appropriate location inside the main function available in <strong>c</strong>.</li>

 <li>The client and server functionality need to be implemented in files <strong>c </strong>and <strong>task1_server.c</strong>, respectively.</li>

 <li>In <strong>c </strong>file, implement the calculate function that the server will invoke whenever required.</li>

 <li>Run <strong>make task1 </strong>command from the root folder of this assignment to get binary file named <strong>task1_calc</strong>. Use this binary to test the functionality of your implementation.</li>

</ul>

You can use below mentioned APIs to implement this part of the assignment. Refer to man page of these APIs to know about their usage.

<table width="286">

 <tbody>

  <tr>

   <td width="120">pipe</td>

   <td width="120">write</td>

   <td width="45">strcmp</td>

  </tr>

  <tr>

   <td width="120">close</td>

   <td width="120">sprintf</td>

   <td width="45">sscanf</td>

  </tr>

  <tr>

   <td width="120">wait</td>

   <td width="120">strtok</td>

   <td width="45">exit</td>

  </tr>

  <tr>

   <td width="120">read</td>

   <td width="120">strcmp</td>

   <td width="45"> </td>

  </tr>

 </tbody>

</table>

Figure 2: Flow of establishing chat communication between two user.

<h2>Task 2: Lets Chit-Chat !!! Chat Between Two Users</h2>

In this task, you need to implement chat communication between two users using pipe. The main process acts as the driver and creates two child processes to facilitate communication between them using pipes. Each child processes (i.e. user-1 and user-2) exec the same “user program” binary to start the conversation between them. User program reads the chat content which has to be communicated to the other user from the <strong>chat content </strong>file (provided) and writes the chat content received from other user to the <strong>store content </strong>file.

Figure 2 shows the workflow of this chat communication. One of the users will be the <strong>initiator </strong>based upon the first line (<strong>keyword: initiate</strong>) in the <strong>chat content </strong>file. The initiator user will start the chat by sending next line (actual message) after initiate keyword in the <strong>chat content </strong>file. Similar to the initiator, any user can be the <strong>terminator </strong>of chat communication. Terminator will have <strong>keyword:</strong>

<strong>bye </strong>in the chat content file or there is no content left for communication in the <strong>chat content </strong>file.

As part of this task, you need to implement both driver and user program. The driver is responsible for fork &amp; exec the user programs and establishing the communication channels between them. The user program is responsible for reading the chat messages and writing the replies as mentioned above. The driver program should accept 4 command line arguments as follows.

<strong>./task2_driver &lt;user1_content&gt; &lt;user1_store&gt; &lt;user2_content&gt; &lt;user2_store&gt;</strong>

<h3>Implementation</h3>

<ul>

 <li>Navigate to the <strong>Task-2 </strong>folder of code base, there are two C files, <strong>c </strong>and <strong>task2_user.c</strong>, to implement the driver and user program, respectively.</li>

 <li>After implementation, run the <strong>make task2 </strong>command from the root folder of this assignment. You will get two binary files at the root folder, namely <strong>task2_driver </strong>and <strong>task2_user</strong>, corresponding to the driver and user programs.</li>

 <li>You need to exec <strong>task2_user </strong>inside the driver program two times to mimic two users.</li>

 <li>Use the <strong>task2_driver </strong>binary as mentioned above to test the correct functionality of your implementation.</li>

 <li>You will find two additional text files for testing purposes, namely— <strong>chat-1.txt </strong>and <strong>chat-2.txt</strong>, inside the <strong>Task-2 </strong>folder, which holds the sample <strong>chat contents </strong>for two users.</li>

 <li>We will push the sample output file (correct <strong>store content </strong>files) in some time to the github repo, You can use these output files to verify your <strong>store content </strong></li>

</ul>

You can use below mentioned APIs to implement this part of the assignment. Refer to man page of these APIs to know about their usage.

<table width="413">

 <tbody>

  <tr>

   <td width="120">pipe</td>

   <td width="120">fopen</td>

   <td width="120">strcmp</td>

   <td width="53">exec</td>

  </tr>

  <tr>

   <td width="120">close</td>

   <td width="120">perror</td>

   <td width="120">sscanf</td>

   <td width="53">strcpy</td>

  </tr>

  <tr>

   <td width="120">wait</td>

   <td width="120">getline</td>

   <td width="120">sscanf</td>

   <td width="53">sprintf</td>

  </tr>

  <tr>

   <td width="120">read</td>

   <td width="120">free</td>

   <td width="120">strlen</td>

   <td width="53">fclose</td>

  </tr>

  <tr>

   <td width="120">write</td>

   <td width="120">fputs</td>

   <td width="120">atoi</td>

   <td width="53">exit</td>

  </tr>

 </tbody>

</table>

<h2>Task 3: Now Secure it !!!! Securing the Chat Communication</h2>

Now you will secure the communication between users that you have implemented in task-2 by encrypting the chat using secure key. Here one of the users will be <strong>initiator </strong>as in task-2 based upon the first line (<strong>keyword: initiate</strong>) in the <strong>chat content </strong>file. The <strong>initiator </strong>will have secure key as the second line in the <strong>chat content </strong>file. The <strong>initiator </strong>will send this secure key as first message in the chat communication. The other user (non initiator) will have secure key as first line in her corresponding <strong>chat content </strong>file and will send this as first message to initiator after receiving key from the initiator. All further communication between these two users will be encrypted by their on key. i.e. initiator will send all his messages from third line on wards in <strong>chat content </strong>file by encrypting using his key, same way non-initiator will send all her messages encrypted using her key. Secure key will have two components <strong>key_a </strong>and <strong>key_b</strong>. Both these components of key can hold any value between <strong>0 </strong>to <strong>25</strong>. The format of line which contains secure key inside the <strong>chat content </strong>file is <strong>KEY key_a Key_b</strong>.

On receiving encrypted message, the users should write messages both encrypted and decrypted version of the messages to their respective <strong>store content </strong>files. Similar to the initiator, any user can be the <strong>terminator </strong>of chat communication. Terminator will have <strong>keyword: bye </strong>in the chat content file or there is no content left for communication in the <strong>chat content </strong>file.

Same as task-2, you need to implement both driver and user program. The driver is responsible for fork &amp; exec the user programs and establishing the communication channels between them. The user program is responsible for reading the chat messages and writing the replies as mentioned above. The driver program should accept 4 command line arguments as follows.

<strong>./task3_driver &lt;user1_content&gt; &lt;user1_store&gt; &lt;user2_content&gt; &lt;user2_store&gt;</strong>

<h3>Implementation</h3>

<ul>

 <li>Navigate to the <strong>Task-3 </strong>folder of code base, you will find two C files, <strong>c </strong>and <strong>task3_user.c</strong>, to implement the driver and user program, respectively.</li>

 <li>Run the <strong>make task3 </strong>command from the root folder of this assignment. You will get two binary files at the root folder, <strong>task3_driver </strong>and <strong>task3_user</strong>, corresponding to the driver and user program.</li>

 <li>Exec <strong>task3_user </strong>inside the driver program two times to mimic two users same as in task-2.</li>

 <li>Use the <strong>task3_driver </strong>binary as mentioned above to test the correct functionality of your implementation.</li>

 <li>For testing purposes, there are two additional text files, <strong>chat-1.txt </strong>and <strong>chat-2.txt </strong>inside the <strong>Task-3 </strong>folder, these hold the sample <strong>chat contents </strong>for two users.</li>

 <li>We will push the sample output file (correct <strong>store content </strong>files) in some time to the github repo, You can use these output files to verify your <strong>store content </strong></li>

 <li>For the encryption and decryption process, you may use the <strong>decryptMessage(char msg[], KEYS key, size_t length) </strong>and <strong>encryptMessage(char msg[], KEYS key, size_t length) </strong>custom-built function which is available in crypt.c file inside the Task-3 folder itself.</li>

</ul>

<strong>More information on encrypt/decrypt functions (provided ):</strong>

These functions take three arguments—(i) <strong>msg: </strong>a message to encrypt/decrypt, (ii) <strong>KEYS key: </strong>key to be used for encryption/decryption process, and (iii) <strong>length: </strong>the length of the message. These functions will take encrypted/decrypted messages on the msg buffer and return the decrypted/encrypted message on the same buffer. Here, <strong>KEYS </strong>is a C structure that holds both key components to be used for the encryption and decryption process. The declaration and usage of the <strong>KEYS </strong>structure are as follows:

/* Declaration */ typedef struct{ int key_a; int key_b;

} KEYS;

/* usage */

KEYS key;                             //declaration of KEYS type variable.

key.key_a = 2; // Setting the first component key_a of key key.key_b = 10; // Setting the second component key_b of key

You can use below mentioned APIs to implement this part of the assignment. Refer to man page of

these APIs to know about their usage.

<table width="413">

 <tbody>

  <tr>

   <td width="120">pipe</td>

   <td width="120">fopen</td>

   <td width="120">strcmp</td>

   <td width="53">exec</td>

  </tr>

  <tr>

   <td width="120">close</td>

   <td width="120">perror</td>

   <td width="120">sscanf</td>

   <td width="53">strcpy</td>

  </tr>

  <tr>

   <td width="120">wait</td>

   <td width="120">getline</td>

   <td width="120">sscanf</td>

   <td width="53">sprintf</td>

  </tr>

  <tr>

   <td width="120">read</td>

   <td width="120">free</td>

   <td width="120">strlen</td>

   <td width="53">fclose</td>

  </tr>

  <tr>

   <td width="120">write</td>

   <td width="120">fputs</td>

   <td width="120">atoi</td>

   <td width="53">exit</td>

  </tr>

 </tbody>

</table>