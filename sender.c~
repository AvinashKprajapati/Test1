#include<stdio.h>
#include<sys/socket.h>
#include<sys/types.h>
#include<netinet/in.h>
#include<string.h>
#include<stdlib.h>
#include<arpa/inet.h>
#include<math.h>

#define SIZE 7

// sender function 

int sender (int b[10],int k)
 {
    int checksum,sum=0,i;
        printf("\nSENDER\n");
     
for(i=0;i<k;i++)
      sum+=b[i];
      printf("SUM IS: %d",sum);
                     
    checksum=~sum;
    printf("\nSENDER's CHECKSUM IS:%d",checksum);
    return checksum;
 }
//receiver

  int receiver(int c[10],int k,int scheck)
  {
     int checksum,sum=0,i;
     printf("\n\n RECEIVER\n");
     for(i=0;i<k;i++)
      sum+=c[i];
      printf(" RECEIVER SUM IS:%d",sum);
      sum=sum+scheck;
      checksum=~sum;
      printf("\nRECEIVER's CHECKSUM IS:%d",checksum);
      return checksum;
  }
 
int main()
{  int a[10],k,m,scheck,rcheck;
     printf("\nENTER SIZE OF THE String");
     scanf("%d",&m);
     printf("\nENTER THE  THE ARRAY:");
     for(k=0;k<m;k++)
    scanf("%d",&a[k]);
    scheck=sender(a,m);
    rcheck=receiver(a,m,scheck);
    if(rcheck==0)
      printf("\n\nNO ERROR IN TRANSMISSION\n\n");
    else
      printf("\n\nERROR DETECTED");





        int sfd,lfd,len,i,j,status;
        char str[20],frame[20],temp[20],ack[20];
        struct sockaddr_in saddr,caddr;
        sfd=socket(AF_INET,SOCK_STREAM,0);
        if(sfd<0)
                perror("Error");
                bzero(&saddr,sizeof(saddr));
                saddr.sin_family=AF_INET;
                saddr.sin_addr.s_addr=htonl(INADDR_ANY);
                saddr.sin_port=htons(5465);
                if(bind(sfd,(struct sockaddr*)&saddr,sizeof(saddr))<0)
                        perror("Bind Error");
                listen(sfd,5);
                len=sizeof(&caddr);
                lfd=accept(sfd,(struct sockaddr*)&caddr,&len);
                printf(" Enter the text : \n");
                scanf("%s",str);
                i=0;
                while(i<strlen(str))
                {
                        memset(frame,0,20);
                        strncpy(frame,str+i,SIZE);
                        printf(" Transmitting Frames. ");
                        len=strlen(frame);
                        for(j=0;j<len;j++)
                        {
                                 printf("%d",i+j);
                                 sprintf(temp,"%d",i+j);
                                 strcat(frame,temp);
                        }
                        printf("\n");
                        write(lfd,frame,sizeof(frame));
                        read(lfd,ack,20);
                        sscanf(ack,"%d",&status);
                        if(status==-1)
                                printf(" Transmission issuccessful. \n");
                        else
                        {
                                printf(" Received error in %d\n\n",status);
                                printf("\n\n RetransmittingFrame. ");
                                for(j=0;;)
                                {
                                         frame[j]=str[j+status];
                                         printf("%d",j+status);
                                         j++;
                                     if((j+status)%1==0)
                                                 break;
                                }
                                printf("\n");
                                frame[j]='\0';
                                len=strlen(frame);
                                for(j=0;j<len;j++)
                                {
sprintf(temp,"%d",j+status);
                                         strcat(frame,temp);
                                }
                                write(lfd,frame,sizeof(frame));
                        }
                        i+=SIZE;
                }
                write(lfd,"exit",sizeof("exit"));
                printf("Exiting\n");
                sleep(2);
                close(lfd);
                close(sfd);
}

