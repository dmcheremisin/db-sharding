# Create tables
crete table grades_parts(id serial not null, g int not null) partition by range(g);
create table g0035 (like grades_parts including indexes)
create table g3560 (like grades_parts including indexes)
create table g6080 (like grades_parts including indexes)
create table g80100 (like grades_parts including indexes)

# Attach partitions to main table
alter table grades_parts attach partition g0035 for values from (0) to (35);
alter table grades_parts attach partition g3560 for values from (35) to (60);
alter table grades_parts attach partition g6080 for values from (60) to (80);
alter table grades_parts attach partition g80100 for values from (80) to (100);

