Create a Python SSH client for Termux with these specifications:

1. **Connection Profiles**  
   - Store profiles in JSON format (`~/.ssh_commander.json`)  
   - Profile fields: `name`, `host`, `port`, `user`, `auth_type` (key/password), `key_path` (optional)  
   - Encryption for stored passwords using `cryptography`  

2. **Profile Management CLI**  
   - Commands:  
     ```bash
     ssh-commander add-profile  # Interactive setup
     ssh-commander list         # Show saved profiles
     ssh-commander remove <name>
     ```

3. **SSH Execution**  
   - Use `paramiko` for SSH connections  
   - Support both key-based and password auth  
   - Command execution:  
     ```bash
     ssh-commander run <profile> "df -h"
     ```

4. **Macro System**  
   - Store command sequences in profiles:  
     ```json
     "macros": {
        "status": ["uptime", "df -h", "free -m"]
     }
     ```
   - Execute macros: `ssh-commander macro <profile> status`  

5. **Session Features**  
   - Real-time output streaming  
   - Save session logs to `~/ssh_logs/<profile>_<timestamp>.log`  
   - Timeout handling (10s default)  

6. **Termux Integration**  
   - Detect SSH keys in `~/.ssh/`  
   - Handle Android permission issues  
   - Minimal dependencies (`paramiko`, `cryptography`)  

7. **UI/UX**  
   - Color-coded output (commands=cyan, output=white, errors=red)  
   - Connection status indicators  
   - Interactive mode for manual command entry  

8. **Error Handling**  
   - Network unreachable  
   - Authentication failures  
   - Missing dependencies 

9. **GitHub & Cli**
    - Create a README.md of this project
    - Always make a new branch and push on GitHub.
    ```
    git init
    git add .
    git commit -m "<commit-name>"
    git branch -M main
    git remote add origin https://github.com/rkstudio585/SSH-Remote.git
    git push -u origin main
    ```

Required: Implement `--help` documentation and usage examples.
