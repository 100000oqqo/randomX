import psutil

def close_application(application_name):
    for process in psutil.process_iter(['pid', 'name']):
        if process.info['name'] == application_name:
            pid = process.info['pid']
            try:
                process = psutil.Process(pid)
                process.terminate()
                print(f"Closed {application_name} (PID: {pid}) successfully.")
            except psutil.NoSuchProcess:
                print(f"Process {pid} not found.")
            except psutil.AccessDenied:
                print(f"Access denied to terminate {application_name} (PID: {pid}).")
            break
    else:
        print(f"{application_name} not found running.")

# Example: Close Notepad
close_application("ChatGPT")
