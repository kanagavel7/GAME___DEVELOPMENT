# EX 6 : Two-Dimensional Transformations

## AIM

To write a c program to implement 2D transformation of image.


## ALGORITHM

Step 1:Start the program.

Step 2:Draw the image with default parameters.

Step 3 : Get the choice from the user.

Step 4: Get the parameters for transformation.

Step 5 : Perform the transformation.

Step 6 : Draw the image.

Step 7 : Stop the program.


## Program :

```
#include<stdio.h>
#include<graphics.h>
//#include<process.h>

void main()
{
    int gd = DETECT, gm;
    float i, xmax, ymax, xmin, ymin, x11, y11, x22, y22, m;
    float a[4], b[4], c[4], x1, y1;

    clrscr();
    initgraph(&gd, &gm, "C:\\TURBOC3\\BGI");

    printf("\nEnter the bottom-left coordinate of viewport: ");
    scanf("%f %f", &xmin, &ymin);

    printf("\nEnter the top-right coordinate of viewport: ");
    scanf("%f %f", &xmax, &ymax);

    rectangle(xmin, ymin, xmax, ymax);

    printf("\nEnter the coordinates of 1st end point of line: ");
    scanf("%f %f", &x11, &y11);

    printf("\nEnter the coordinates of 2nd endpoint of line: ");
    scanf("%f %f", &x22, &y22);

    line(x11, y11, x22, y22);

    for(i = 0; i < 4; i++)
    {
        a[i] = 0;
        b[i] = 0;
    }

    m = (y22 - y11) / (x22 - x11);

    if(x11 < xmin) a[3] = 1;
    if(x11 > xmax) a[2] = 1;
    if(y11 < ymin) a[1] = 1;
    if(y11 > ymax) a[0] = 1;

    if(x22 < xmin) b[3] = 1;
    if(x22 > xmax) b[2] = 1;
    if(y22 < ymin) b[1] = 1;
    if(y22 > ymax) b[0] = 1;

    printf("\nRegion code of 1st pt ");
    for(i = 0; i < 4; i++)
    {
        printf("%f", a[i]);
    }

    printf("\nRegion code of 2nd pt ");
    for(i = 0; i < 4; i++)
    {
        printf("%f", b[i]);
    }

    printf("\nAnding : ");
    for(i = 0; i < 4; i++)
    {
        c[i] = a[i] && b[i];
    }

    for(i = 0; i < 4; i++)
        printf("%f", c[i]);

    getch();

    if((c[0] == 0) && (c[1] == 0) && (c[2] == 0) && (c[3] == 0))
    {
        if((a[0] == 0) && (a[1] == 0) && (a[2] == 0) && (a[3] == 0) &&
           (b[0] == 0) && (b[1] == 0) && (b[2] == 0) && (b[3] == 0))
        {
            clrscr();
            clearviewport();
            printf("\nThe line is totally visible\nand not a clipping candidate");
            rectangle(xmin, ymin, xmax, ymax);
            line(x11, y11, x22, y22);
            getch();
        }
        else
        {
            clrscr();
            clearviewport();
            printf("\nLine is partially visible");
            rectangle(xmin, ymin, xmax, ymax);
            line(x11, y11, x22, y22);
            getch();

            if((a[0] == 0) && (a[1] == 1))
            {
                x1 = x11 + (ymin - y11) / m;
                x11 = x1;
                y11 = ymin;
            }
            else if((b[0] == 0) && (b[1] == 1))
            {
                x1 = x22 + (ymin - y22) / m;
                x22 = x1;
                y22 = ymin;
            }

            if((a[0] == 1) && (a[1] == 0))
            {
                x1 = x11 + (ymax - y11) / m;
                x11 = x1;
                y11 = ymax;
            }
            else if((b[0] == 1) && (b[1] == 0))
            {
                x1 = x22 + (ymax - y22) / m;
                x22 = x1;
                y22 = ymax;
            }

            if((a[2] == 0) && (a[3] == 1))
            {
                y1 = y11 + m * (xmin - x11);
                y11 = y1;
                x11 = xmin;
            }
            else if((b[2] == 0) && (b[3] == 1))
            {
                y1 = y22 + m * (xmin - x22);
                y22 = y1;
                x22 = xmin;
            }

            if((a[2] == 1) && (a[3] == 0))
            {
                y1 = y11 + m * (xmax - x11);
                y11 = y1;
                x11 = xmax;
            }
            else if((b[2] == 1) && (b[3] == 0))
            {
                y1 = y22 + m * (xmax - x22);
                y22 = y1;
                x22 = xmax;
            }

            clrscr();
            clearviewport();
            printf("\nAfter clippling:");
            rectangle(xmin, ymin, xmax, ymax);
            line(x11, y11, x22, y22);
            getch();
        }
    }
    else
    {
        clrscr();
        clearviewport();
        printf("\nLine is invisible");
        rectangle(xmin, ymin, xmax, ymax);
        getch();
    }

    closegraph();
    getch();
}

```

## Output :

<img width="553" height="441" alt="Screenshot 2025-09-26 104127" src="https://github.com/user-attachments/assets/2bc7a56f-a63d-49d3-aea8-ad763580351a" />

<img width="534" height="435" alt="Screenshot 2025-09-26 104138" src="https://github.com/user-attachments/assets/55884fa4-5aa2-48b1-abf6-8866a9ff3c0c" />

<img width="533" height="438" alt="Screenshot 2025-09-26 104144" src="https://github.com/user-attachments/assets/afc71aa9-0f6b-4bda-8a91-92f73c3224e2" />

## Result :

Thus the C program to implement Line Clipping for all the cases using Region Code was written and executed successfully.
