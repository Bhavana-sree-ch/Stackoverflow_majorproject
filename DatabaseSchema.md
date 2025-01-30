**Database Schema for Stack Overflow**

### **Entities:**

1. **Users**
   - user_id (Primary Key)
   - username (Unique, Not Null)
   - email (Unique, Not Null)
   - password_hash (Not Null)
   - created_at (Default: Current Timestamp)

2. **Tags**
   - tag_id (Primary Key)
   - tag_name (Unique, Not Null)
   - description

3. **Questions**
   - question_id (Primary Key)
   - user_id (Foreign Key → Users)
   - title (Not Null)
   - body (Not Null)
   - created_at (Default: Current Timestamp)
   - updated_at (Default: Current Timestamp)
   - votes (Default: 0)

4. **Answers**
   - answer_id (Primary Key)
   - question_id (Foreign Key → Questions)
   - user_id (Foreign Key → Users)
   - body (Not Null)
   - created_at (Default: Current Timestamp)
   - updated_at (Default: Current Timestamp)
   - votes (Default: 0)

5. **QuestionTags**
   - question_id (Foreign Key → Questions)
   - tag_id (Foreign Key → Tags)
   - (Primary Key → Combination of question_id, tag_id)

6. **Comments**
   - comment_id (Primary Key)
   - user_id (Foreign Key → Users)
   - question_id (Foreign Key → Questions, Nullable)
   - answer_id (Foreign Key → Answers, Nullable)
   - body (Not Null)
   - created_at (Default: Current Timestamp)

7. **Votes**
   - vote_id (Primary Key)
   - user_id (Foreign Key → Users)
   - question_id (Foreign Key → Questions, Nullable)
   - answer_id (Foreign Key → Answers, Nullable)
   - vote_type (Allowed Values: -1, 1)
   - created_at (Default: Current Timestamp)

### **Relations Between Entities:**
- A **User** can ask multiple **Questions**.
- A **User** can answer multiple **Questions**.
- A **Question** can have multiple **Answers**, but an **Answer** belongs to only one **Question**.
- A **Question** can have multiple **Tags**, and a **Tag** can be associated with multiple **Questions** (Many-to-Many).
- A **User** can leave multiple **Comments** on both **Questions** and **Answers**.
- A **User** can upvote/downvote **Questions** and **Answers**.
- **Votes** are linked to either **Questions** or **Answers**, but not both at the same time.
