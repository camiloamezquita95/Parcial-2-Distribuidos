build:
	@docker build -t desarrolloparcial_db 
start:
	@docker run -d -p 5433:5432 --name parcial2db desarrolloparcial_db
delete:
	@docker rm -f parcial2db
inside:
	@docker run -it -p 5433:5432 --name parcial2db desarrolloparcial_db   /bin/bash
test:
	@delete
	@build
	@start
        
