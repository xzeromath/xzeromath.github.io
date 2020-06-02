---
# layout: "post"
title: "excelfile_export"
date: "2017-08-09 10:44"
# categories: Django
tag: Django
header:
  teaser: /assets/images/4.png

---

## 장고에서 엑셀파일로 export하는 view 예시

{% highlight python %}
def excel(request):
    import io
    import xlsxwriter
    response = HttpResponse(content_type='application/vnd.ms-excel')
    response['Content-Disposition'] = 'attachment; filename=Report.xlsx'
    output = io.BytesIO()
    workbook = xlsxwriter.Workbook(output)

    # 엑셀파일 편집부분--------
    from accounts.models import Profile
    li=Profile.objects.all()
    # workbook=xlsxwriter.Workbook('datatest3.xlsx')
    worksheet=workbook.add_worksheet()
    row=1
    col=0
    for i in li:
        worksheet.write(row,col,str(i.user))
        worksheet.write(row,col+1,i.phone_number)
        worksheet.write(row,col+2,i.address)
        worksheet.write(row,col+3,i.class_number)
        worksheet.write(row,col+4,i.user.email)
        row+=1
    workbook.close()
    # ----------엑셀파일편집부분 끝

    xlsx_data = output.getvalue()
    response.write(xlsx_data)
    return response

{% endhighlight %}
