# pagination_Nextjs


#### initialize the page, get the page value from url and set to state
```
const [pageSelected, setPageSelected] = useState(1);
  useEffect(() => {
    if(!router.query.page){
      router.push({ pathname: router.pathname, query: { page: 1  } });     
    }else{
      setPageSelected(router.query.page);     
    }
  },[]);
  ```
  
  #### update the url when state updated
  ```  
  useEffect(() => {
    router.push({ pathname: router.pathname, query: { page: pageSelected  } });     
  },[pageSelected]);
  ```
  
  #### update the state when page changes
  ```  
  const onChange = (e) => {         
    setPageSelected(e);
  }

  ```
  
  #### Pagination component
  ```
   <Pagination current={Number(pageSelected)} total={trending?.pager?.total_items} onChange={onChange} />  
  ```
