# wordCount
wc
#include "stdafx.h"
#include "stdio.h"
#include "stdlib.h"
#include "string.h"

void CharCount();  //字符统计函数
void WordCount();  //单词统计函数
void LineCount();  //行数统计函数
void Muiltiple();  //综合统计函数，包括代码行，空行，注释行

int main(int argc,char *argv[])
{
    if ((strcmp(argv[1], "-c") == 0) && (strcmp(argv[2], "file.c") == 0))
    {
        CharCount();
    }
    
    if ((strcmp(argv[1], "-w") == 0) && (strcmp(argv[2], "file.c") == 0))
    
        WordCount();
    }
    if ((strcmp(argv[1], "-l") == 0) && (strcmp(argv[2], "file.c") == 0))
    {
        LineCount();
    }
    if ((strcmp(argv[1], "-a") == 0) && (strcmp(argv[2], "file.c") == 0))
    {
        Muiltiple();
    }
    return 0;


}

void CharCount() //字符统计函数
{
    FILE *fp;
    int c = 0;
    char ch;
    if((fp = fopen("file.c","r")) == NULL)
    {
        printf("file read failure.");
    }
    ch = fgetc(fp);
    while(ch != EOF)
    {
            c ++;
            ch = fgetc(fp);
    }
    printf("char count is ：%d.\n",c);
    fclose(fp);
}

void WordCount() //单词统计函数
{
    FILE *fp;
    int w = 0;
    char ch;
    if((fp = fopen("file.c","r")) == NULL)
    {
        printf("file read failure.");
    }
    ch = fgetc(fp);
    while(ch != EOF)
    {
        if ((ch >= 'a'&&ch <= 'z')||(ch >= 'A'&&ch <='Z')||(ch >= '0'&&ch <= '9'))
        {
            while ((ch >= 'a'&&ch <= 'z')||(ch >= 'A'&&ch <= 'Z')||(ch >= '0'&&ch <= '9')||ch == '_')
            {
                ch = fgetc(fp);
            }
            w ++;
            ch = fgetc(fp);    
        }
        else 
        {
            ch = fgetc(fp);
        }
    }
    printf("word count is ：%d.\n",w);
    fclose(fp);

}

void LineCount() //行数统计函数
{
    FILE *fp;
    int l = 1;
    char ch;
    if((fp = fopen("file.c","r")) == NULL)
    {
        printf("file read failure.");
    }
    ch = fgetc(fp);
    while(ch != EOF)
    {
        if (ch == '\n')
        {
            l ++;
            ch = fgetc(fp);
        }
        else
        {
            ch = fgetc(fp);
        }
    }
    printf("line count is ：%d.\n",l);
    fclose(fp);
}

void Muiltiple()  //综合统计函数，包括代码行，空行，注释行
{
    FILE *fp;
    char ch;
    int c=0,e=0,n=0;
    if((fp = fopen("file.c","r")) == NULL)
    {
        printf("file read failure.");
    }
    ch = fgetc(fp);
    while(ch != EOF)
    {
        if (ch == '{'||ch == '}')
        {
            e ++;
            ch = fgetc(fp);
        }
        else if (ch == '\n')
        {
            ch = fgetc(fp);
            while(ch == '\n')
            {
                e ++;
                ch = fgetc(fp);
            }
        }
        else if (ch == '/')
        {
            ch = fgetc(fp);
            if (ch == '/')
                while(ch != '\n')
                {
                    ch = fgetc(fp);
                }
                n ++;
                ch = fgetc(fp);
        }
        else
        {
            c ++;
            while (ch != '{'&&ch != '}'&&ch != '\n'&&ch != '/'&&ch != EOF)
            {
                ch = fgetc(fp);
            }
        }

    }
    printf("code line count is ：%d.\n",c);
    printf("empt line count is ：%d.\n",e);
    printf("note line count is ：%d.\n",n);
    fclose(fp);
}
