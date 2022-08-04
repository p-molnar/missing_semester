DIR_NAME	=	missing
FILE_NAME	=	semester
FILE_NAME2	=	last-modified.txt

FILE		= 	$(DIR_NAME)/$(FILE_NAME)
LAST_MOD	=	$(DIR_NAME)/$(FILE_NAME2)

YELLOW		=	\033[1;33m
DEF			=	\033[0m

solution:
	@printf "$(YELLOW)create a new directory called \`missing\`$(DEF)\n"
	mkdir -p $(DIR_NAME)
	@printf "\n"

	@printf "$(YELLOW)creating new file \`$(FILE_NAME)\` under \`$(DIR_NAME)\`$(DEF)\n"
	touch $(FILE)
	@printf "\n"

	@printf "$(YELLOW)writing into \`$(FILE_NAME)\`$(DEF)\n"
	echo "#!/bin/sh" > $(FILE)
	echo "curl --head --silent https://missing.csail.mit.edu" >> $(FILE)
	@printf "\n"

	@printf "$(YELLOW)attempting to execute \`$(FILE)\`$(DEF)\n"
	./$(FILE)
	@printf "\n"

	@printf "$(YELLOW)get info on \`$(FILE)\`$(DEF)\n"
	ls -l $(FILE)
	@printf "\n"

	@printf "$(YELLOW)execute \`$(FILE)\` with \`sh\` interpreter$(DEF)\n"
	sh $(FILE)
	@printf "\n"

	@printf "$(YELLOW)change execution rights of \`$(FILE)\`$(DEF)\n"
	chmod u=+rwx $(FILE)
	@printf "\n"

	@printf "$(YELLOW)write the 'last modified' date output by \`$(FILE)\` into \`$(LAST_MOD)\`$(DEF)\n"
	ls -l $(FILE) | awk '{ printf("%s %s %s\n", $$6, $$7, $$8) }' > $(LAST_MOD)
	@printf "\n"

clean:
	@printf "$(YELLOW)removing all$(DEF)\n"
	rm -rf $(DIR_NAME)

re: clean
	make -i solution