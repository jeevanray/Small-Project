# Small-Project


query_partyMain ='''insert  INTO Partymain(TenantID, CreatedOn, Country, Pincode, City, State, Address)
 VALUES (?, ?, ?,?,?, ?,?)'''
#labels =['TenantID', 'CreatedOn', 'Country', 'Pincode', 'City', 'State', 'Address']
party_main = [] \n
for _,x in df1.iterrows(): \n
     #y = dict(zip(labels,x)) \n
    lst = list(x) \n
    
    
    cursor.execute('''select *  from PartyMain where TenantID = ? and City = ? and Address=?''',(lst[0], lst[4],lst[6]))
    if not cursor.fetchall():
        cursor.execute(query_partyMain,lst)
        print('executed success')
        cursor.commit()
        cursor.execute('''select MainPartyID  from PartyMain where TenantID = ? and City = ? and Address=?''',(lst[0], lst[4],lst[6]))
        x = cursor.fetchone()
        party_main.append(x[0])
        
    else:
        print('failed')
