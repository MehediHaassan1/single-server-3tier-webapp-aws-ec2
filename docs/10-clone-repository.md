# Clone GitHub Repository on EC2

## 1. What is Git clone?
Git clone is the process of copying a remote Git repository (like GitHub) into a local machine or server.

In this case, we clone the backend project into our EC2 instance.

---

## 2. Why we need to clone repo?
- Get application code on server
- Deploy backend on EC2
- Keep code version controlled via GitHub
- Easy updates and rollback

---

## 3. Prerequisites
Before cloning:
- Git must be installed
- Node.js environment ready
- GitHub repository must exist

---

## 4. Install Git (if not installed)

```bash id="git-install"
sudo apt update
sudo apt install git -y
```

## 5. Configure Git (optional but recommended)
```
git config --global user.name "your-username"
git config --global user.email "your-email@example.com"
```

## 6. Clone Repository

### HTTPS method:
```
git clone https://github.com/username/repository-name.git
```

### SSH method (advanced):
```
git clone git@github.com:username/repository-name.git
```

## 7. Move into project directory
```
cd repository-name
```

## 8. Verify files
```
ls
```

## 9. What I achieved

### After cloning:
- Application source code is available on EC2
- Ready for dependency installation
- Ready for deployment

## 10. Next Step

### After cloning repo:
- Install dependencies (npm install)
- Configure environment variables
- Run application using PM2