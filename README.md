# Bug Tracker Application

first create dir strucutre
create a venv in bug-tracker backend
activate it
install requirements here only: pip install -r requirements.txt
to write all requirements to file: pip freeze >requirements.txt


to  get dir structure:
# Set the path to your project root here
$ProjectRoot = "C:\bug-tracker\bug-tracker-backend"

# List of exact names to exclude (folders/files)
$exclude = @(
    ".git", ".env", ".env.example", ".gitignore", ".bug-tracker",
    ".venv", "env", "__pycache__", ".mypy_cache", ".pytest_cache",
    ".idea", ".vscode", "lib", "site-packages", "pycache"
)

function Show-Tree {
    param([string]$Path, [string]$Indent = "")

    Get-ChildItem -LiteralPath $Path | Where-Object {
        $exclude -notcontains $_.Name
    } | Sort-Object Name | ForEach-Object {
        $item = $_
        Write-Host "$Indent├── $($item.Name)"
        if ($item.PSIsContainer) {
            Show-Tree -Path $item.FullName -Indent ("$Indent│   ")
        }
    }
}

Show-Tree -Path $ProjectRoot


first install and create alembic init 
run  alembic revision --autogenerate -m "initial"  
then alembic upgrade head

now create models 
and run :alembic revision --autogenerate -m "Initial tables: users, projects, issues" and then alembic upgrade head
tables created in db successfully