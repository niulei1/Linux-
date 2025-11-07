#include<stdlib.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/wait.h>
int main()
{
   int n;
   int p-c[2];
   int c-p[2];
   pid_t pid;
   char line[MAX];
   if(pipe(p-c)<0)
   {
      perror("pipe");
      exit(1);
   }
   if(pipe(c-p)<0)
   {
      perror("error");
      exit(1);
   } 
   if((pid=fork())<0)
   {
     perror("fork");
     exit(1); 
   }
   if(pid>0) 
   {
     close(p-c[0]);
     close(c-p[1]);
     write(p-c[1],"hello",20);
     printf("perent sent: hello\n");
     n= read(c-p[0],line,MAX);
     line[n]='\0';
     printf("P received:%s",line);
     wait(NULL);
     close(p-c[1]); 
     close(p-c[0]);
}
   else
     {
      close(p-c[1]); 
      close(c-p[0]);
      n= read(p-c[0],line,MAX);
      line[n]='\0';
      printf("C received:%s",line);
      write(c-p[1],"hello",20);
      printf("child sent: hello\n);
      close(p-c[0]); 
      close(c-p[1]);
     }
    return 0;
   }
